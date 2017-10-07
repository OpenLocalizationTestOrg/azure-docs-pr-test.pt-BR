---
title: "aaaInstall SAP HANA no SAP HANA no Azure (instâncias grandes) | Microsoft Docs"
description: "Como tooinstall HANA SAP em um HANA SAP no Azure (instância grande)."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Como tooinstall e configure o SAP HANA (instâncias grandes) no Azure

A seguir estão algumas definições importantes tooknow antes de ler este guia. Em [Visão geral e arquitetura do SAP HANA (instâncias grandes) no Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture), apresentamos duas classes diferentes de unidades de Instância Grande do HANA com:

- S72, S72m, S144, S144m, S192 e S192m, que chamamos tooas Olá ', classe de tipo' de SKUs.
- S384, S384m, S384xm, S576, S768 e S960, que chamamos tooas Olá 'Classe de tipo II' de SKUs.

especificador de classe Olá é contínuo toobe usado Olá HANA instância grande documentação tooeventually consulte toodifferent recursos e requisitos com base em SKUs do HANA grande instância.

Outras definições que usamos frequentemente são:
- **Grande carimbo da instância:** uma pilha de infraestrutura de hardware que é o SAP HANA TDI certificada e dedicado de instâncias do SAP HANA toorun dentro do Azure.
- **SAP HANA no Azure (instâncias grande):** nome oficial da oferta de saudação em instâncias do HANA toorun do Azure no SAP HANA TDI certified hardware que é implantado em carimbos de instância grande em diferentes regiões do Azure. Olá relacionados ao termo **instância grande HANA** é curta para o SAP HANA no Azure (instâncias grandes) e é amplamente usada neste guia de implantação técnica.


instalação de saudação do SAP HANA é sua responsabilidade e você pode iniciar atividade Olá após a entrega de um novo SAP HANA no servidor do Azure (instâncias grandes). E, depois de conectividade de saudação entre o Azure VNet(s) e Olá instância grande HANA unidades foi estabelecida. 

> [!Note]
> Por política SAP, instalação de saudação do SAP HANA deve ser executada por uma pessoa certificada tooperform instalações do SAP HANA. Uma pessoa, o que passou exame Certified associar de tecnologia SAP hello, exames de certificação de instalação do SAP HANA, ou por um certificado pela SAP integrador de (SI).

Verificar novamente, especialmente ao planejar tooinstall HANA 2.0, [2235581 de n º de observação de suporte do SAP - SAP HANA: sistemas operacionais com suporte](https://launchpad.support.sap.com/#/notes/2235581/E) em ordem toomake-se de que Olá sistema operacional tem suporte com hello SAP HANA versão você decidiu tooinstall. Você percebe que Olá SO com suporte para HANA 2.0 é mais restrito do sistema operacional com suporte do HANA 1.0 hello. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Primeiras etapas após o recebimento da saudação HANA grandes unidades de instância

**Primeiro etapa** após o recebimento Olá instância grande HANA e ter estabelecido instâncias toohello de conectividade e acesso, é tooregister Olá SO da instância de saudação com seu provedor de sistema operacional. Esta etapa inclui registrando o SO Linux SUSE em uma instância do SUSE SMT que você precisa toohave implantado em uma VM no Azure. unidade de instância grande HANA Olá pode se conectar a instância SMT toothis (consulte mais adiante nesta documentação). Ou o sistema de operacional RedHat precisa toobe registrado com hello Red Hat assinatura Manager, é necessário tooconnect para. Consulte também os comentários neste [documento](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Esta etapa também é necessário toobe toopatch capaz de saudação sistema operacional. Uma tarefa que é de responsabilidade de saudação do cliente hello. Para o SUSE, encontrar documentação tooinstall e configure SMT [aqui](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Segunda etapa** é toocheck para novas atualizações e correções de saudação específico versão/versão do sistema operacional. Verifique se o nível do patch de saudação da saudação instância grande HANA está no estado mais recente hello. Com base no tempo no patch/versões e alterações toohello imagem do sistema operacional que Microsoft pode implantar, pode haver casos onde patches mais recentes Olá não podem ser incluídos. Assim é uma etapa obrigatória depois de assumir uma unidade de instância grande HANA toocheck se patches relevantes para segurança e desempenho, disponibilidade e funcionalidade lançadas enquanto isso pelo fornecedor específico de Linux Olá e precisam toobe aplicado.

**Terceira etapa** é toocheck out Olá Observações sobre o SAP relevantes para instalar e configurar o SAP HANA Olá específico versão/versão do sistema operacional. Devido a tooSAP recomendações ou alterações de toochanging anotações ou configurações que são dependentes de cenários de instalação individuais, Microsoft nem sempre será capaz de toohave uma unidade de instância grande HANA configurada perfeitamente. Portanto, é obrigatório para você como um cliente, tooread Olá Observações sobre o SAP relacionado tooSAP HANA na sua versão exata do Linux. Também verifique as configurações de Olá Olá SO/versão necessárias e aplique as configurações de saudação quando não tiver feito isso.

Especificamente, verifique Olá parâmetros a seguir e, eventualmente, ajustada para:

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

Começando com o SP1 SLES12 e RHEL 7.2, esses parâmetros devem ser definidos em um arquivo de configuração no diretório de /etc/sysctl.d hello. Por exemplo, um arquivo de configuração com o nome de saudação 91-NetApp-HANA.conf deve ser criado. Para versões mais antigas do SLES e RHEL, esses parâmetros devem ser definidos como in/etc/sysctl.conf.

Para RHEL todas as versões e a partir do SLES12, Olá 
- sunrpc.tcp_slot_table_entries = 128

parâmetro deve ser definido como in/etc/modprobe.d/sunrpc-local.conf. Se não existir um arquivo hello, primeiro devem ser criado, adicionando Olá a seguinte entrada: 
- options sunrpc tcp_max_slot_table_entries=128

**Quarta etapa** é toocheck Olá a hora do sistema de sua unidade de instância grande HANA. Olá instâncias são implantadas com um fuso horário do sistema que representa o local de saudação do Olá Olá de região do Azure em que HANA grande carimbo da instância está localizado. Você é livre toochange Olá sistema tempo ou fuso horário de instâncias de saudação que você possui. Ao fazer isso e ordenação mais instâncias em seu locatário, prepare-se de que você precisa de fuso horário Olá tooadapt do hello entregues recentemente instâncias. Operações do Microsoft não tem nenhum ideias sobre fuso horário sistema Olá que configurar com instâncias de saudação após passar hello. Portanto instâncias implantadas recentemente podem não estar definidas no hello mesmo fuso horário como Olá um alterado para. Como resultado, é sua responsabilidade como toocheck de cliente e se for necessário adaptar Olá fuso horário de instância (s) de saudação entregue. 

**Quinta etapa** é toocheck etc/hosts. Como obtenham entregue folhas hello, eles têm diferentes endereços IP atribuídos para finalidades diferentes (consulte a próxima seção). Verifique no arquivo hello etc/hosts. Em casos onde as unidades são adicionadas a um locatário existente, não espera toohave etc/hosts dos sistemas Olá implantado recentemente mantidos corretamente com endereços IP hello anteriormente sistemas entregues. Portanto, é você como configurações corretas de saudação do cliente toocheck, que uma instância implantada recentemente pode interagir e resolver nomes de saudação de anteriormente implantados unidades no seu locatário. 

## <a name="networking"></a>Rede
Vamos supor que você seguiu as recomendações de saudação projetar seus VNets do Azure e conectar-se às instâncias do VNets toohello HANA grandes conforme descrito nesses documentos:

- [Visão geral e arquitetura do SAP HANA (instâncias grandes) no Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infraestrutura e conectividade do SAP HANA (instâncias grandes) no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Há alguns detalhes vale a pena toomention sobre a rede de saudação de unidades único hello. Cada unidade de instância grande HANA vem com dois ou três endereços IP atribuídos tootwo ou três portas NIC de unidade de saudação. Três endereços IP são usados em configurações em expansão HANA e cenário de replicação de sistema do HANA hello. Um dos endereços IP hello atribuído toohello NIC de unidade hello está fora do hello pool de IP do servidor que foi descrito Olá [visão geral do SAP HANA (instância grande) e arquitetura no Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

distribuição de saudação para as unidades com dois endereços IP atribuídos deve parecer com:

- eth0.xx devem ter um endereço IP atribuído que está fora do intervalo de endereços do Pool de IP do servidor que você enviou tooMicrosoft de saudação. Esse endereço IP deverá ser usado para manter em /etc/hosts de saudação sistema operacional.
- eth1.xx devem ter um endereço IP atribuído que é usado para comunicação tooNFS. Portanto, esses endereços fazer **não** necessário toobe mantida em ordem tooallow instância tooinstance o tráfego dentro do locatário Olá etc/hosts.

Para casos de implantação de Replicação de Sistema do HANA ou de expansão do HANA, uma configuração de folha com dois endereços IP atribuídos não é adequada. Se ter dois endereços IP atribuídos apenas e que desejam toodeploy configuração, entre em contato com SAP HANA no gerenciamento de serviços do Azure tooget um terceiro endereço IP em um terceiro VLAN atribuído. Para unidades de instância grande HANA ter três endereços IP atribuídos em três portas NIC, hello regras de uso a seguir se aplicam:

- eth0.xx devem ter um endereço IP atribuído que está fora do intervalo de endereços do Pool de IP do servidor que você enviou tooMicrosoft de saudação. Portanto, esse endereço IP não deverá ser usado para manter em /etc/hosts de saudação sistema operacional.
- eth1.xx devem ter um endereço IP atribuído que é usado para comunicação tooNFS armazenamento. Portanto, esse tipo de endereço não deve ser mantido em etc/hosts.
- eth2.xx devem ser exclusivamente usado toobe mantido etc/hosts para a comunicação entre instâncias diferentes do hello. Esses endereços também seria endereços IP hello que precisam toobe mantido em configurações em expansão HANA como endereços IP que HANA usa para a configuração de nó entre hello.



## <a name="storage"></a>Armazenamento

Olá layout de armazenamento para o SAP HANA no Azure (instâncias grandes) é configurado pelo SAP HANA no gerenciamento de serviços do Azure por meio do SAP recomendado guias, conforme documentado no [requisitos de armazenamento do SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper. Olá aproximados tamanhos de volumes diferentes Olá com hello diferentes HANA grandes instâncias SKUs foi documentados no [visão geral do SAP HANA (instância grande) e arquitetura no Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

convenções de nomenclatura Olá Olá de volumes de armazenamento estão listadas no Olá a tabela a seguir:

| Uso de armazenamento | Nome da montagem | Nome do volume | 
| --- | --- | ---|
| Dados do HANA | /hana/data/SID/mnt0000<m> | IP de Armazenamento: /hana_data_SID_mnt00001_tenant_vol |
| Log do HANA | /hana/log/SID/mnt0000<m> | IP de Armazenamento: /hana_log_SID_mnt00001_tenant_vol |
| Backup de log do HANA | /hana/log/backups | IP de Armazenamento: /hana_log_backups_SID_mnt00001_tenant_vol |
| HANA compartilhado | /hana/shared/SID | IP de Armazenamento: /hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | IP de Armazenamento: /hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Onde SID = Olá HANA instance ID do sistema 

E locatário = uma enumeração interna das operações durante a implantação de um locatário.

Como você pode ver, HANA compartilhado e usr/sap estão compartilhando Olá mesmo volume. a nomenclatura de pontos de montagem Olá Olá incluem hello ID do sistema de instâncias do HANA hello, bem como o número de montagem hello. Em implantações escaláveis, há somente uma montagem, como mnt00001. Ao contrário da implantação escalável, em que você verá o mesmo número de montagens que os nós de trabalho e mestre. Para o ambiente de expansão hello, dados, log, volumes de backup de log são tooeach compartilhado e anexado nó na configuração de expansão de saudação. Para configurações de execução de várias instâncias do SAP, um conjunto diferente de volumes é a unidade de instância grande HAN toohello criado e anexado.

Como ler o papel hello e pesquisar uma unidade de instância grande HANA, você percebe que unidades Olá vêm com o volume de disco, em vez de amplas para HANA/dados e que temos um volume de log/HANA/backup. motivo Olá por que é dimensionado Olá HANA/dados muito grandes, é que oferecemos para você, como um cliente está usando instantâneos do armazenamento de Olá Olá mesmo volume de disco. Isso significa hello mais armazenamento instantâneos que executar, hello mais espaço é consumido por instantâneos em seus volumes de armazenamento atribuído. volume de backup/de log HANA Olá é não pensamento toobe Olá volume tooput backups de banco de dados no. É toobe dimensionado usada como volume de backup para backups de log de transações do HANA hello. Em futuras versões do armazenamento Olá instantâneo instantâneos de autoatendimento, que têm como destino esse toohave volume específico mais frequentes. E com que mais frequentam replicações toohello recuperação de desastres se desejar toooption-in para a funcionalidade de recuperação de desastres Olá fornecida pela infraestrutura de instância grande HANA hello. Consulte os detalhes em [Alta disponibilidade e recuperação de desastre do SAP HANA (instâncias grandes) no Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 

Além disso toohello armazenamento fornecido, você pode comprar capacidade de armazenamento adicional em incrementos de 1 TB. Esse armazenamento adicional pode ser adicionado como novos volumes tooa HANA grandes instâncias.

Durante a integração com o SAP HANA no gerenciamento de serviços do Azure, o cliente Olá Especifica uma ID de usuário (UID) e a ID de grupo (GID) para o grupo de usuário e sapsys sidadm hello (ex: 1000,500) é necessário que, durante a instalação do sistema SAP HANA de saudação, esses mesmos valores são usados. Como você deseja toodeploy várias instâncias do HANA em uma unidade, você tem vários conjuntos de volumes (um conjunto para cada instância). Como resultado, no momento da implantação, você precisa toodefine:

- Olá SID das instâncias HANA diferentes hello (sidadm é derivado dele).
- Tamanhos de memória de instâncias diferentes de HANA hello. Desde que o tamanho da memória Olá por instâncias define o tamanho de saudação de volumes de saudação em cada conjunto de volumes individual.

Com base nas recomendações do provedor de armazenamento Olá montagem as opções a seguir é configurada para todos os volumes montados (exclui o LUN de inicialização):

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

Esses pontos são configurados em/etc/fstab como Olá mostrada no gráfico a seguir de montagem:

![fstab de volumes montados na unidade de Instância Grande do HANA](./media/hana-installation/image1_fstab.PNG)

saída de saudação do hello comando df -h em uma unidade de instância grande do HANA S72m pareceria com:

![fstab de volumes montados na unidade de Instância Grande do HANA](./media/hana-installation/image2_df_output.PNG)


controlador de armazenamento Hello e nós em carimbos de instância grande Olá são servidores de tooNTP sincronizados. Com você sincronizar Olá SAP HANA em unidades do Azure (instâncias grandes) e máquinas virtuais do Azure em relação a um servidor NTP, deve ser não ocorra de descompasso significativa de tempo entre a infraestrutura de saudação e unidades de saudação de computação no Azure ou instância grande carimbos.

Ordem toooptimize armazenamento do SAP HANA toohello usado abaixo, você também deve definir Olá parâmetros de configuração do SAP HANA a seguir:

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
Para versões do SAP HANA 1.0 backup tooSPS12, esses parâmetros podem ser definidos durante a instalação de saudação do banco de dados do SAP HANA hello, conforme descrito em [2267798 de # nota SAP - configuração de saudação banco de dados do SAP HANA](https://launchpad.support.sap.com/#/notes/2267798)

Você também pode configurar parâmetros de saudação após a instalação de banco de dados do SAP HANA Olá usando Olá hdbparam framework. 

Com o SAP HANA 2.0, estrutura de hdbparam Olá foi preterida. Como resultado, os parâmetros de saudação devem ser definidos usando comandos SQL. Para obter detalhes, consulte [Nota SAP nº 2399079: Eliminação de hdbparam no HANA 2](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>Sistema operacional

Espaço de permuta de saudação entregue a imagem do sistema operacional é definido too2 GB de acordo com o toohello [1999997 de # de observação de suporte do SAP - perguntas Frequentes: SAP HANA memória](https://launchpad.support.sap.com/#/notes/1999997/E). Qualquer configuração de diferentes desejado precisa toobe definido por você como um cliente.

[SUSE Linux Enterprise Server 12 SP1 para aplicativos SAP](https://www.suse.com/products/sles-for-sap/hana) é a distribuição de saudação do Linux instalado para o SAP HANA no Azure (instâncias grandes). Essa distribuição específica fornece recursos específicos do SAP &quot;imediato saudação&quot; (incluindo parâmetros previamente configurados para execução do SAP em SLES efetivamente).

Consulte [recurso de biblioteca e White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) no site SUSE hello e [SAP no SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) em Olá SAP comunidade rede (SCN) para vários recursos úteis relacionados toodeploying SAP HANA em SLES (configuração de saudação incluindo de alta disponibilidade, operações de tooSAP específico de proteção de segurança e muito mais).

Links adicionais e úteis relacionados ao SAP no SUSE:

- [SAP HANA no Site do SUSE Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [Práticas recomendadas para SAP: replicação de enfileiramento – SAP NetWeaver no SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).
- [ClamSAP – proteção antivírus de SLES para SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (incluindo SLES 12 para aplicativos SAP).

Suporte a anotações aplicável tooimplementing SAP HANA em 12 SLES do SAP:

- [Observação de suporte SAP 1944799 – diretrizes SAP HANA para instalação do sistema operacional SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).
- [Observação de suporte SAP 2205917 – configurações do SO recomendadas para o banco de dados do SAP HANA para SLES 12 para aplicativos SAP](https://launchpad.support.sap.com/#/notes/2205917/E).
- [Observação de suporte SAP 1984787 – SUSE Linux Enterprise Server 12: notas de instalação](https://launchpad.support.sap.com/#/notes/1984787).
- [Observação de suporte SAP 171356 – software SAP no Linux: informações gerais](https://launchpad.support.sap.com/#/notes/1984787).
- [Observação de suporte SAP 1391070 – soluções UUID do Linux](https://launchpad.support.sap.com/#/notes/1391070).

[Red Hat Enterprise Linux para SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) é outra oferta para execução do SAP HANA em instâncias grandes de HANA. As versões do RHEL 6.7 e 7.2 estão disponíveis. 

Links adicionais e úteis relacionados a SAP no Red Hat:
- [SAP HANA no site Red Hat Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

Suporte a anotações aplicável tooimplementing SAP HANA no Red Hat do SAP:

- [Nota de Suporte da SAP #2009879 – Diretrizes SAP HANA para o sistema operacional RHEL (Red Hat Enterprise Linux)](https://launchpad.support.sap.com/#/notes/2009879/E).
- [Nota de Suporte da SAP #2292690 - Banco de dados SAP HANA: configurações de sistema operacional recomendadas para RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).
- [Nota de Suporte da SAP #2247020 - Banco de dados SAP HANA: configurações de sistema operacional recomendadas para RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).
- [Observação de suporte SAP 1391070 – soluções UUID do Linux](https://launchpad.support.sap.com/#/notes/1391070).
- [Nota de Suporte da SAP #2228351 - Linux: SAP HANA Database SPS 11 revisão 110 (ou superior) em RHEL 6 ou SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [Nota de Suporte da SAP #2397039 - Perguntas frequentes: SAP em RHEL](https://launchpad.support.sap.com/#/notes/2397039).
- [Nota de Suporte da SAP #1496410 - Red Hat Enterprise Linux 6.x: instalação e atualização](https://launchpad.support.sap.com/#/notes/1496410).
- [Nota de Suporte da SAP #2002167 - Red Hat Enterprise Linux 7.x: instalação e atualização](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Sincronização de horário

Aplicativos do SAP baseados em Olá arquitetura do SAP NetWeaver são confidenciais nas diferenças de tempo para vários componentes que constituem Olá Olá sistema SAP. SAP ABAP curto despejos de memória com o título do erro de saudação do ZDATE\_grande\_tempo\_comparação provavelmente está familiarizado, como esses despejos curtos aparecem quando hello as "se e deslocando é muito" hora do sistema de servidores diferentes ou máquinas virtuais.

Para o SAP HANA no Azure (instâncias grandes), sincronização de hora feita no Azure &#39; t se aplicam a unidades de computação toohello em carimbos de instância grande hello. Essa sincronização não é aplicável à execução de aplicativos SAP em VMs nativas do Azure, pois o Azure garante que a hora do sistema é sincronizada corretamente. Como resultado, um tempo separada servidor deve ser configurado que pode ser usado por servidores de aplicativos SAP em execução em máquinas virtuais do Azure e Olá SAP HANA banco de dados instâncias em execução em instâncias grandes HANA. infraestrutura de armazenamento Olá carimbos de instância grande é sincronizado com servidores NTP do tempo.

## <a name="setting-up-smt-server-for-suse-linux"></a>Configurando o servidor SMT para o SUSE Linux
Instâncias do SAP HANA grandes não tem toohello conectividade direta com a Internet. Assim, ele não é um processo simples de tooregister uma unidade com o provedor do sistema operacional hello e toodownload e aplicar patches. Em caso de saudação do SUSE Linux, uma solução pode ser tooset um servidor SMT em uma VM do Azure. Enquanto Olá VM do Azure precisa toobe hospedado em uma rede virtual do Azure, que é conectado toohello instância grande HANA. Com esse é um servidor SMT, unidade de instância grande HANA Olá pode registrar e baixar patches. 

O SUSE fornece um guia maior em sua [Ferramenta de Gerenciamento de Assinaturas para SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Pré-condição para a instalação de saudação de um servidor SMT que atenda a tarefa Olá para instância grande HANA, você precisará:

- Uma rede virtual do Azure que está conectada toohello circuito HANA grande ER de instância.
- Uma conta SUSE associada a uma organização. Enquanto a organização Olá precisaria toohave alguns assinatura válida do SUSE.

### <a name="installation-of-smt-server-on-azure-vm"></a>Instalação do servidor SMT em uma VM do Azure

Nesta etapa, você deve instalar servidor SMT Olá uma VM do Azure. medida primeiro Olá é toolog em toohello [SUSE cliente Center](https://scc.suse.com/)

Como você está conectado, vá tooOrganization--> as credenciais da organização. Nesta seção, você deve encontrar credenciais Olá necessário tooset servidor SMT de saudação.

Olá terceira etapa é tooinstall uma VM do Linux SUSE no hello VNet do Azure. Olá toodeploy VM, levar a uma imagem da Galeria SLES 12 SP2 do Azure. No processo de implantação hello, não defina um nome DNS e não use endereços IP estáticos visto nesta captura de tela

![implantação da VM no servidor SMT](./media/hana-installation/image3_vm_deployment.png)

Olá VM implantada foi uma VM menor e tem o endereço IP interno de saudação em hello Azure VNet de 10.34.1.4. Nome da saudação VM foi smtserver. Após a instalação de Olá Olá conectividade toohello HANA grandes unidades de instância foi marcada. Depende de como você organizada de resolução de nome talvez seja necessário tooconfigure resolução de unidades de instância grande HANA Olá etc/hosts de saudação VM do Azure. Adicione um toohello em disco adicional VM que vai toobe usado toohold patches de saudação. disco de inicialização de saudação em si pode ser muito pequeno. No caso de Olá demonstrado, disco Olá foi montado muito/srv/www/htdocs conforme Olá captura de tela a seguir. Um disco de 100 GB deve ser suficiente.

![implantação da VM no servidor SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Faça logon toohello instância grande HANA unidades, manter /etc/hosts e verifique se você pode alcançar Olá VM do Azure que supostamente server do toorun Olá SMT pela rede hello.

Após essa verificação é feita com êxito, será necessário toolog na VM do Azure que deve executar o servidor SMT de saudação do toohello. Se você estiver usando putty toolog em toohello VM, você precisa tooexecute esta sequência de comandos na janela de bash:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Depois de executar esses comandos, reinicie suas configurações de saudação tooactivate bash. Depois, inicie o YAST.

No YAST, vá tooSoftware manutenção e procure smt. Selecione smt, que alterna tooyast2 smt automaticamente, conforme mostrado abaixo

![SMT no yast](./media/hana-installation/image5_smt_in_yast.PNG)


Aceite a seleção de saudação para instalação em smtserver hello. Uma vez instalado, vá a configuração do servidor SMT toohello e insira credenciais organizacionais saudação do hello SUSE cliente Center recuperado anteriormente. Também inserir seu nome de host de VM do Azure como Olá SMT URL do servidor. Nesta demonstração, era https://smtserver conforme exibido no gráfico próximo hello.

![Configuração do servidor SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Como a próxima etapa, você precisa tootest se Olá conexão toohello SUSE cliente Center funciona. Como você pode ver no hello seguintes gráficos, em caso de demonstração de Olá, ele funcionou.

![Teste se conectar tooSUSE cliente Center](./media/hana-installation/image7_test_connect.png)

Uma vez Olá SMT do início da instalação, você precisa tooprovide uma senha de banco de dados. Como é uma nova instalação, você precisa toodefine essa senha, conforme mostrado no gráfico próximo hello.

![Definir a senha do banco de dados](./media/hana-installation/image8_define_db_passwd.PNG)

interação de Avançar Olá que tiver é quando um certificado é criado. Passar pelo diálogo hello, como mostrado a seguir e etapa Olá deve continuar.

![Criar um certificado para o servidor SMT](./media/hana-installation/image9_certificate_creation.PNG)

Pode haver alguns minutos gastos na etapa de saudação do 'Executar verificação de sincronização' no final de saudação da configuração de saudação. Após a instalação de saudação e configuração do servidor SMT hello, você deve encontrar o repositório de diretório Olá em Olá montagem ponto /srv/www/htdocs/mais alguns subdiretórios no repositório. 

Reinicie o servidor do hello SMT e seus serviços relacionados com esses comandos.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Download de pacotes no servidor SMT

Depois que todos os hello serviços são reiniciados, selecione Olá pacotes adequados no gerenciamento SMT usando Yast. seleção do pacote Hello depende na imagem do sistema operacional de saudação do servidor de instância grande HANA hello e não Olá SLES versão ou versão do servidor Olá VM em execução Olá SMT. Um exemplo de tela de seleção de saudação é mostrado abaixo.

![Selecionar pacotes](./media/hana-installation/image10_select_packages.PNG)

Quando tiver terminado com a seleção do pacote hello, será necessário cópia inicial do toostart saudação do servidor do hello selecionar pacotes toohello SMT que você configurar. Essa cópia é acionada no shell de saudação usando Olá comando smt espelhamento conforme mostrado abaixo


![Baixar pacotes tooSMT server](./media/hana-installation/image11_download_packages.PNG)

Como ver acima, os pacotes de saudação devem copiados em diretórios Olá criados sob Olá montagem ponto /srv/www/htdocs. Esse processo pode levar algum tempo. Dependente de quantos pacotes que você selecionar, pode levar até tooone hora ou mais.
Como esse processo for concluído, você precisa de instalação do cliente toomove toohello SMT. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Configurar Olá SMT cliente em unidades de instância grande HANA

Olá clientes neste caso são unidades de instância grande HANA de saudação. instalação de servidor SMT Olá copiados Olá script clientSetup4SMT.sh em Olá VM do Azure. Copie o script sobre toohello unidade instância grande HANA você deseja tooconnect tooyour SMT servidor. Iniciar o script hello com a opção -h hello e dê a ele como o nome do parâmetro saudação do servidor SMT. Neste exemplo, smtserver.

![Configurar o cliente SMT](./media/hana-installation/image12_configure_client.PNG)

Pode haver um cenário onde hello carga do certificado de saudação do servidor de saudação pelo cliente Olá foi bem-sucedida, mas falha no registro da saudação conforme mostrado abaixo.

![Falha no registro do cliente](./media/hana-installation/image13_registration_failed.PNG)

Se a falha no registro de hello, ler este [documento de suporte do SUSE](https://www.suse.com/de-de/support/kb/doc/?id=7006024) e execute as etapas de saudação descritas lá.

> [!IMPORTANT] 
> Como nome do servidor é necessário tooprovide nome de saudação de saudação VM, no smtserver neste caso, sem nome de domínio totalmente qualificado de saudação. Apenas saudação VM nome funciona. 

Depois que essas etapas foram executadas, você precisa Olá tooexecute comando a seguir na unidade de instância grande HANA Olá

```
SUSEConnect –cleanup
```

> [!Note] 
> Em nossos testes, sempre tínhamos toowait alguns minutos após essa etapa. Olá clientSetup4SMT.sh execução imediata, após hello medidas corretivas descritas em Olá artigo SUSE, terminou com mensagens que certificado Olá não será válido ainda. Geralmente, aguardar de 5 a 10 minutos e executar clientSetup4SMT.sh terminou com uma configuração de cliente bem-sucedida.

Se você executou o problema Olá necessário toofix com base em etapas de saudação do artigo SUSE Olá, é necessário clientSetup4SMT.sh toorestart na unidade de instância grande HANA Olá novamente. Agora ele deverá ser concluído com êxito, conforme mostrado abaixo.

![Registro do cliente bem-sucedido](./media/hana-installation/image14_finish_client_config.PNG)

Com essa etapa, você configurou o cliente SMT Olá Olá instância grande HANA unidade tooconnect no servidor SMT Olá instalado no hello VM do Azure. Agora você pode colocar 'zypper backup' ou 'zypper em' tooinstall OS patches tooHANA grandes instâncias ou instalar outros pacotes. É entendido que você só pode obter patches que você baixou antes no servidor SMT hello.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Exemplo de uma instalação do SAP HANA nas Instâncias Grandes do HANA
Esta seção ilustra como tooinstall SAP HANA em uma unidade de instância grande HANA. estado de início Olá temos aparência:

- Fornecida toodeploy de dados Olá todos os Microsoft é uma instância grande do SAP HANA.
- Olá instância grande do SAP HANA foi recebido da Microsoft.
- Você criou uma rede virtual do Azure que é a rede de local tooyour conectado.
- Conectado circuito ExpressRotue Olá HANA grandes instâncias toohello VNet do Azure.
- Você instalou uma VM do Azure usada como uma jumpbox para as Instâncias Grandes do HANA.
- Certificar-se que você pode conectar da unidade de instância grande HANA Olá salto caixa tooyour e vice-versa.
- Você verificado se todos os pacotes necessários de hello e patches estão instalados.
- Você ler Observações sobre o SAP hello e documentação sobre instalação do HANA em Olá sistema operacional você está usando e certificar-se de que versão do HANA Olá de escolha é suportado na versão Olá sistema operacional.

O que é mostrado nas sequências de Avançar Olá é download Olá Olá HANA instalação pacotes toohello salto caixa VM, nesse caso, executada em um sistema de operacional Windows, a cópia de saudação da unidade de instância grande HANA Olá pacotes toohello e a sequência de saudação da instalação de saudação do.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Download de bits de instalação do SAP HANA Olá
Como unidades de instância grande HANA Olá não tem toohello conectividade direta com a internet, você não pode diretamente baixar pacotes de instalação de saudação do toohello do SAP HANA grande instância VM. tooovercome Olá ausente conectividade direta da internet, você precisa de caixa de salto hello. Baixe o hello pacotes toohello salto caixa VM.

Pacotes de instalação do HANA ordem toodownload Olá, é necessário um usuário de S SAP ou outro usuário, o que permite que você tooaccess Olá Marketplace do SAP. Siga esta sequência de telas após o logon:

Vá muito[SAP Service Marketplace](https://support.sap.com/en/index.html) > clique em Download de Software > instalações e atualização > por índice alfabético > em H – SAP HANA Platform Edition > SAP HANA plataforma Edition 2.0 > Instalação > Olá de Download arquivos a seguir

![Baixar a instalação do HANA](./media/hana-installation/image16_download_hana.PNG)

No caso de demonstração de Olá, baixamos pacotes de instalação do SAP HANA 2.0. Na caixa de salto do Azure Olá VM, você expandir arquivos autoextraível Olá no diretório Olá conforme mostrado abaixo.

![Extrair a instalação do HANA](./media/hana-installation/image17_extract_hana.PNG)

Como Olá arquivos forem extraídos, copie o diretório de saudação criado por extração hello, no caso de Olá acima 51052030, unidade de instância grande HANA toohello no volume de /hana/shared Olá em um diretório que você criou.

> [!Important]
> Não copiar pacotes de instalação de saudação na raiz de saudação ou LUN de inicialização, desde que o espaço é limitado e precisa toobe usada por outros processos também.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Instalar o SAP HANA na unidade de instância grande HANA Olá
Em ordem tooinstall SAP HANA, você precisa toolog em como raiz do usuário. Somente raiz tem suficiente tooinstall permissões SAP HANA.
Olá primeira coisa toodo é tooset permissões no diretório Olá que você copiou em hana/compartilhado. precisam de permissões de saudação tooset como

```
chmod –R 744 <Installation bits folder>
```

Se você quiser tooinstall SAP HANA usando Olá gráfica de instalação, Olá gtk2 pacote necessidades toobe instalado Olá HANA grandes instâncias. Verifique se ele está instalado com o comando Olá

```
rpm –qa | grep gtk2
```

Mais etapas, estamos demonstrando o instalação do SAP HANA Olá com interface gráfica do usuário de saudação. Como a próxima etapa, vá para o diretório de instalação hello e navegue no subdiretório Olá HDB_LCM_LINUX_X86_64. Iniciar

```
./hdblcmgui 
```
fora desse diretório. Agora você está obtendo guiado por meio de uma sequência de telas nos onde você precisa de dados de saudação do tooprovide para instalação de saudação. No caso de Olá demonstrado, podemos está instalando o servidor de banco de dados do SAP HANA hello e componentes de cliente do SAP HANA hello. Portanto, nossa seleção é “Banco de Dados do SAP HANA”, conforme mostrado abaixo

![Selecionar o HANA na instalação](./media/hana-installation/image18_hana_selection.PNG)

Na próxima tela de saudação, você escolhe Olá opção 'Instalar o novo sistema'

![Selecionar a nova instalação do HANA](./media/hana-installation/image19_select_new.PNG)

Após essa etapa, você precisa tooselect entre vários componentes adicionais que podem ser instalados adicionalmente servidor de banco de dados do SAP HANA toohello.

![Selecionar os componentes adicionais do HANA](./media/hana-installation/image20_select_components.PNG)

Para finalidade de Olá desta documentação, podemos escolher Olá SAP HANA cliente e Olá SAP HANA Studio. Também instalamos uma instância escalável. Portanto, na próxima tela de Olá, você precisa toochoose 'Host único System' 

![Selecionar a instalação escalável](./media/hana-installation/image21_single_host.PNG)

Na próxima tela de saudação, você precisa tooprovide alguns dados

![Fornecer o SID do SAP HANA](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Como HANA sistema SID (ID), você precisa tooprovide Olá mesmo SID, como Microsoft é fornecido quando você solicitou a implantação de instância grande HANA hello. Escolher um SID diferente torna a instalação de saudação falhar devido a problemas de permissão tooaccess em diferentes volumes, Olá

Como o diretório de instalação você usar o diretório de /hana/shared hello. Na próxima etapa de saudação, você precisa tooprovide locais de saudação para arquivos de dados do HANA hello e arquivos de log do HANA Olá


![Fornecer o local do Log do HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Você deve definir como arquivos de log e dados Olá volumes que já vêm com pontos de montagem de saudação que contêm Olá SID que você escolheu na seleção de tela de saudação antes desta tela. Se Olá SID incompatibilidade com hello um digitado, na tela hello antes, volte e ajuste Olá SID toohello valor em pontos de montagem de saudação.

Na próxima etapa de hello, examine o nome do host hello e, eventualmente, corrigi-lo. 

![Examinar o nome do host](./media/hana-installation/image24_review_host_name.PNG)

Na próxima etapa de Olá, você também precisa tooretrieve dados deu tooMicrosoft quando ordenada implantação de instância grande HANA hello. 

![Fornecer um UID e GID do usuário do sistema](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Você precisa tooprovide Olá mesmo ID de usuário do sistema e a ID do grupo de usuários, como Microsoft é fornecido como ordem de implantação de unidade de saudação. Se você não toogive Olá muito IDs mesmo, instalação de saudação do SAP HANA na unidade de instância grande HANA Olá falhará.

Em Olá duas telas, que não estamos mostrando nesta documentação, você precisa tooprovide senha de saudação para o usuário do sistema de saudação do banco de dados do SAP HANA Olá e a senha de saudação do usuário de sapadm de Olá, que é usado para Olá SAP Host Agent que é instalado como parte do instância de banco de dados do SAP HANA Hello.

Depois de definir senha hello, uma tela de confirmação aparece. Verifique todos os dados de saudação listados e continuam com a instalação de saudação. Acessar uma tela de progresso documentos Olá progresso da instalação, como Olá abaixo

![Verificar o progresso da instalação](./media/hana-installation/image27_show_progress.PNG)

Como Olá instalação for concluída, você deve uma imagem como Olá seguindo um

![A instalação é concluída](./media/hana-installation/image28_install_finished.PNG)

Neste ponto, instância do SAP HANA Olá deve ser ligado e em execução e pronto para uso. Você deve ser capaz de tooconnect tooit do SAP HANA Studio. Também, certifique-se de que você verifique para os patches mais recentes do SAP HANA hello e aplica esses patches.
























































 







 




