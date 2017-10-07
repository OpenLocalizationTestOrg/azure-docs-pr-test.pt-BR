---
title: aaaDesign e implementar um Oracle banco de dados no Azure | Microsoft Docs
description: Projete e implemente um banco de dados Oracle no seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Projete e implemente um banco de dados Oracle no Azure

## <a name="assumptions"></a>Suposições

- Você está planejando toomigrate um banco de dados Oracle de tooAzure local.
- Você tem uma compreensão de saudação várias métricas em relatórios AWR Oracle.
- Você tem uma compreensão das linha de base do desempenho de aplicativo e da utilização da plataforma.

## <a name="goals"></a>Metas

- Entender como toooptimize sua implantação do Oracle no Azure.
- Explorar as opções de ajuste de desempenho para um banco de dados Oracle em um ambiente do Azure.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Olá diferenças entre um local e a implementação do Azure 

A seguir estão algumas importantes tookeep coisas em mente ao migrar aplicativos tooAzure local. 

Uma diferença importante é que, em uma implementação do Azure, recursos como VMs, discos e redes virtuais são compartilhados entre outros clientes. Além disso, os recursos podem ser acelerados com base nos requisitos de saudação. Em vez de nos concentrarmos no evitando falha MTBF (), Azure mais destina sobreviventes falha hello (MTTR).

Olá tabela a seguir lista algumas das diferenças de saudação entre uma implementação de local e uma implementação do Azure de um banco de dados Oracle.

> 
> |  | **Implementação local** | **Implementação no Azure** |
> | --- | --- | --- |
> | **Rede** |LAN/WAN  |SDN (Rede definida por software)|
> | **Grupo de segurança** |Ferramentas de restrições de IP/porta |[NSG (Grupo de Segurança de Rede)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Resiliência** |MTBF (tempo médio entre falhas) |MTTR (toorecovery tempo médio)|
> | **Manutenção planejada** |Aplicação de patch/upgrades|[Conjuntos de disponibilidade](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (aplicação de patch/upgrades gerenciados pelo Azure) |
> | **Recurso** |Dedicado  |Compartilhado com outros clientes|
> | **Regiões** |Datacenters |[Pares de regiões](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Armazenamento** |SAN/discos físicos |[Armazenamento gerenciado pelo Azure](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Escala** |Escala vertical |Escala horizontal|


### <a name="requirements"></a>Requisitos

- Determine a taxa de tamanho e crescimento do banco de dados de saudação.
- Determine requisitos de IOPS hello, que você pode estimar com base em Oracle AWR relatórios ou outra ferramentas de monitoramento de rede.

## <a name="configuration-options"></a>Opções de configuração

Há quatro áreas possíveis que você pode ajustar o desempenho de tooimprove em um ambiente do Azure:

- Tamanho da máquina virtual
- Taxa de transferência de rede
- Tipos e configurações de disco
- Configurações de cache de disco

### <a name="generate-an-awr-report"></a>Gerar um relatório AWR

Se você tiver um banco de dados Oracle existente e estiver planejando toomigrate tooAzure, você tem várias opções. Você pode executar Olá Oracle AWR relatório tooget Olá métricas (IOPS, Mbps, GiBs e assim por diante). Em seguida, escolha Olá que VM com base nas métricas de saudação coletados. Ou você pode contatar a infra-estrutura team tooget semelhante de informações.

Considere a execução do relatório AWR durante cargas de trabalho regulares e de pico para poder comparar a diferença. Com base nesses relatórios, você pode dimensionar Olá VMs com base na carga de trabalho média hello ou carga de trabalho máxima hello.

A seguir está um exemplo de como toogenerate um relatório AWR:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Métricas-chave

Seguem as métricas de Olá Olá relatório AWR pode ser obtido:

- Número total de núcleos
- Velocidade de clock da CPU
- Memória total em GB
- Utilização da CPU
- Pico da taxa de transferência de dados
- Taxa de alterações de E/S (leitura/gravação)
- Taxa de log da fase refazer (MBPs)
- Taxa de transferência de rede
- Taxa de latência de rede (baixa/alta)
- Tamanho do banco de dados em GB
- Bytes recebidos por meio do SQL * Net da / tooclient

### <a name="virtual-machine-size"></a>Tamanho da máquina virtual

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Estimar o tamanho da VM com base no uso de CPU, memória e e/s de saudação relatório AWR

Uma coisa que você poderá examinar é Olá principais cinco atingiu o tempo em primeiro plano eventos que indicam onde estão os gargalos de sistema hello.

Por exemplo, em Olá diagrama a seguir, sincronização de arquivos de log de saudação é na parte superior da saudação. Ele indica o número de saudação de esperas são necessários antes de saudação LGWR grava o arquivo de log de refazer Olá log buffer toohello. Esses resultados indicam que há a necessidade de armazenamento ou discos com um desempenho melhor. Além disso, o diagrama de saudação também mostra número Olá da CPU (núcleos) e a quantidade de saudação de memória.

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/cpu_memory_info.png)

Olá diagrama a seguir mostra Olá total e/s de leitura e gravação. Não havia 59 ler e 247.3 GB gravadas durante o tempo de saudação do relatório de saudação.

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Escolher uma VM

Com base nas informações de saudação que você coletou da saudação relatório AWR, a saudação próxima etapa é toochoose uma VM de tamanho similar que atenda às suas necessidades. Você pode encontrar uma lista de VMs disponíveis no artigo Olá [otimizada de memória](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Ajustar tamanho da VM de saudação com uma série VM semelhante com base em Olá ACU

Depois que você escolheu Olá VM, preste atenção toohello ACU para Olá VM. Você pode escolher uma VM diferente com base em Olá valor ACU que melhor atenda às suas necessidades. Para saber mais, confira [Unidade de computação do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Captura de tela da página de unidades ACU Olá](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Taxa de transferência de rede

Olá diagrama a seguir mostra uma relação entre a taxa de transferência e IOPS hello:

![Captura de tela da taxa de transferência](./media/oracle-design/throughput.png)

taxa de transferência de rede total Olá é calculada com base em Olá informações a seguir:
- Tráfego SQL*Rede
- MBps x número de servidores (fluxo de saída, como o Oracle Data Guard)
- Outros fatores, como replicação de aplicativo

![Captura de tela da saudação SQL * Net taxa de transferência](./media/oracle-design/sqlnet_info.png)

Com base nos seus requisitos de largura de banda de rede, há vários tipos de gateway para você toochoose do. Entre eles basic, VpnGw e Azure ExpressRoute. Para obter mais informações, consulte Olá [página de preços de gateway VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Recomendações**

- Latência de rede é a implantação de local de tooan em comparação com o mais alto. Reduzir as viagens de ida e volta da rede pode melhorar significativamente o desempenho.
- tooreduce viagens, consolidar aplicativos que têm transações alta ou aplicativos "tagarelas" em hello mesma máquina virtual.

### <a name="disk-types-and-configurations"></a>Tipos e configurações de disco

- *Discos padrão do SO*: esses tipos de disco oferecem dados persistentes e cache. Eles são otimizados para acesso de SO na inicialização, e não foram projetados para cargas de trabalho transacionais ou de data warehouse (analíticas).

- *Não gerenciado discos*: com esses tipos de disco, você gerenciar as contas de armazenamento de saudação que armazenam arquivos de disco rígido virtual (VHD) de saudação que correspondem a tooyour discos de VM. Os arquivos VHD são armazenados como blobs de páginas nas contas de armazenamento do Azure.

- *Discos gerenciado*: o Azure gerencia contas de armazenamento Olá que você pode usar para os discos VM. Especifique o tipo de disco da saudação (padrão ou premium) e o tamanho de saudação do disco de saudação que você precisa. Azure cria e gerencia disco Olá para você.

- *Discos de armazenamento premium*: esses tipos de disco são ideais para cargas de trabalho de produção. Premium armazenamento dá suporte a discos de VM que podem ser anexado a série toospecific tamanho VMs, como as VMs da série DS, série DSv2, GS e F. discos de premium Olá vem com tamanhos diferentes e você pode escolher entre os discos que variam de too4 de 32 GB, 096 GB. Cada tamanho de disco tem suas próprias especificações de desempenho. Dependendo dos requisitos de aplicativo, você pode anexar um ou mais discos tooyour VM.

Quando você cria um novo disco gerenciado do portal hello, você pode escolher Olá **tipo de conta** para o tipo de saudação do disco que você deseja toouse. Tenha em mente que nem todos os discos disponíveis são mostrados no menu suspenso de saudação. Depois de escolher um tamanho VM específico, menu Olá mostra o armazenamento de premium disponível de saudação somente SKUs com base no tamanho da VM.

![Captura de tela da página de disco gerenciado Olá](./media/oracle-design/premium_disk01.png)

Para saber mais, confira [Armazenamento Premium de alto desempenho e discos gerenciados para VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Depois de configurar o armazenamento em uma máquina virtual, talvez você queira discos de saudação do tooload teste antes de criar um banco de dados. Saber a taxa de e/s de saudação em termos de latência e taxa de transferência pode ajudá-lo a determinar se o suportam a VMs Olá Olá esperado a produtividade com destinos de latência.

Existem diversas ferramentas para realizar o teste de carga do aplicativo, como Oracle Orion, Sysbench e Fio.

Execute o teste de carga de saudação novamente depois que você implantou um banco de dados Oracle. Iniciar suas cargas de trabalho de pico e regulares e Olá Mostrar resultados Olá da linha de base do seu ambiente.

Talvez seja mais importante do armazenamento de saudação toosize com base na taxa de IOPS de saudação em vez de tamanho de armazenamento de saudação. Por exemplo, se Olá necessário IOPS é 5.000, mas você só precisa de 200 GB, discos de premium Olá P30 classe ainda pode obter, embora ele vem com mais de 200 GB de armazenamento.

taxa de IOPS Olá pode ser obtida Olá relatório AWR. Ele é determinado pelo log de refazer hello, leituras físicas e a taxa de gravações.

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/awr_report.png)

Por exemplo, o tamanho de refazer Olá é 12,200,000 bytes por segundo, que é igual too11.63 MBPs.
Olá IOPS é 12,200,000 / 2,358 = 5,174.

Depois de ter uma visão clara dos requisitos de e/s hello, você pode escolher uma combinação de unidades que são mais adequado toomeet esses requisitos.

**Recomendações**

- Para dados de espaço de tabela, distribuir cargas de trabalho de e/s de saudação em um número de discos usando armazenamento gerenciado ou Oracle ASM.
- À medida que aumenta o tamanho de bloco hello e/s para operações de leitura intensa e com uso intensivo de gravação, adicione mais discos de dados.
- Aumente o tamanho do bloco Olá processos sequenciais grandes.
- Use a e/s tooreduce de compactação de dados (para dados e índices).
- Separe os logs da fase refazer, sistema e temps e desfaça o TS em discos de dados separados.
- Não coloque arquivos de aplicativo em discos do SO padrão (/dev/sda). Esses discos são otimizados inicializações rápidas de VM, e talvez não forneçam um bom desempenho para seu aplicativo.

### <a name="disk-cache-settings"></a>Configurações de cache de disco

Há três opções para o cache de host:

- *Somente leitura*: todas as solicitações são armazenadas em cache para leituras futuras. Todas as gravações são persistentes tooAzure diretamente o armazenamento de Blob.

- *Leitura e gravação*: este é um algoritmo de “leitura antecipada”. Olá leituras e gravações em cache para futuras leituras. Gravações de write-through não são persistidos cache local toohello primeiro. Para o SQL Server, gravações são persistente tooAzure armazenamento porque ela usa a gravação. Ele também fornece o menor latência de disco Olá para cargas de trabalho leves.

- *Nenhum* (desabilitado): ao usar essa opção, você pode ignorar o cache de saudação. Todos os dados de saudação toodisk transferido e persistentes tooAzure armazenamento. Isso proporciona método hello mais alta taxa de e/s para cargas de trabalho intensivas de e/s. Você também precisa tootake "custo de transações" em consideração.

**Recomendações**

taxa de transferência toomaximize hello, recomendamos que você inicie com **nenhum** para caching de host. Para o armazenamento Premium, tenha em mente que você deve desabilitar barreiras"hello" ao montar o sistema de arquivos Olá Olá **ReadOnly** ou **nenhum** opções. Atualize arquivo /etc/fstab de saudação com discos de toohello UUID hello.

Para saber mais, veja [Armazenamento Premium para VMs Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Captura de tela da página de disco gerenciado Olá](./media/oracle-design/premium_disk02.png)

- Para discos do sistema operacional, use o cache de **Leitura/Gravação** padrão.
- Para SYSTEM, TEMP e UNDO, use **Nenhum** para o cache.
- Para DATA, use **Nenhum** para armazenar em cache. Porém, se o banco de dados for somente leitura ou leitura intensiva, use o cache de **Somente leitura**.

Depois que a configuração de disco de dados é salvo, você não pode alterar a configuração de cache de host de saudação, a menos que você desmontar a unidade de saudação em Olá nível do sistema operacional e, em seguida, remonte-lo depois de ter feito Olá alterar.


## <a name="security"></a>Segurança

Depois de você ter instalado e configurado o seu ambiente do Azure, Olá próxima etapa é toosecure sua rede. Veja algumas recomendações:

- *Política de NSG*: o NSG pode ser definido por uma sub-rede ou NIC. É mais simples acesso toocontrol no nível de sub-rede Olá para segurança e forçar o roteamento para coisas como firewalls de aplicativo.

- *Jumpbox*: para um acesso mais seguro, os administradores devem não conectar-se diretamente toohello serviço de aplicativo ou banco de dados. Um jumpbox é usado como uma mídia entre a máquina do administrador de saudação e recursos do Azure.
![Captura de tela da página de topologia Olá Jumpbox](./media/oracle-design/jumpbox.png)

    máquina de administrador Olá deve oferecer acesso restrito por IP somente jumpbox de toohello. Olá jumpbox deve ter acesso toohello aplicativo e banco de dados.

- *Rede privada* (sub-redes): É recomendável que você tenha o serviço de aplicativo hello e banco de dados em sub-redes separadas, para melhor controle pode ser definido por diretiva NSG.


## <a name="additional-reading"></a>Leitura adicional

- [Configurar o Oracle ASM](configure-oracle-asm.md)
- [Configurar o Oracle Data Guard](configure-oracle-dataguard.md)
- [Configurar o Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Backup e recuperação do Oracle](oracle-backup-recovery.md)

## <a name="next-steps"></a>Próximas etapas

- [Tutorial: criar VMs altamente disponíveis](../../linux/create-cli-complete.md)
- [Explorar exemplos da CLI do Azure de implantação de VM](../../linux/cli-samples.md)
