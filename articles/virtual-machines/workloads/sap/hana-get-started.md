---
title: "Início rápido: a instalação manual de instância única SAP HANA em máquinas virtuais do Azure | Microsoft Docs"
description: "Guia de início rápido para a instalação manual do SAP HANA de instância única em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Início rápido: instalação manual do SAP HANA de instância única em VMs do Azure
## <a name="introduction"></a>Introdução
Esta guia ajuda você a configurar o SAP HANA de instância única em máquinas virtuais (VMs) do Azure, ao instalar o SAP NetWeaver 7.5 e SAP HANA 1.0 SP12 manualmente. Olá foco deste guia é implantando HANA SAP no Azure. Ele não substitui a documentação do SAP. 

>[!Note]
>Esta guia descreve as implantações do SAP HANA em VMs do Azure. Para obter informações sobre a implantação do SAP HANA em instâncias grandes do HANA, confira [Como usar SAP no Azure em máquinas virtuais (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Pré-requisitos
Esta guia pressupõe que você está familiarizado com tais infraestruturas como, por exemplo, serviços básicos (Iaas):
 * Como máquinas virtuais de toodeploy ou redes virtuais por meio de Olá portal do Azure ou o PowerShell.
 * Olá plataforma cruzada do Azure de linha de comando CLI (interface), incluindo modelos do hello opção toouse notação JSON (JavaScript Object).

Esta guia também pressupõe que você está familiarizado com:
* HANA SAP e SAP NetWeaver e como tooinstall-los no local.
* Instalação e operação do SAP HANA e instâncias de aplicativos SAP no Azure.
* Olá conceitos e procedimentos a seguir:
   * Como planejar a implantação de SAP no Azure, incluindo o planejamento de rede virtual do Azure e o uso do armazenamento do Azure. Confira [SAP NetWeaver em máquinas virtuais (VMs) do Azure — Guia de planejamento e implementação](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Implantação princípios e as maneiras toodeploy VMs no Azure. Confira [Implantação de máquinas virtuais do Azure para SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Alta disponibilidade para o SAP NetWeaver ASCS (Central de Serviços SAP ABAP), o SCS (Central de Serviços SAP) e ERS (liquidação de recebimento avaliado) no Azure. Confira [Alta disponibilidade do SAP NetWeaver em VMs do Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Obter detalhes sobre como tooimprove eficiência na utilização de uma instalação de vários SID do ASCS/SCS no Azure. Confira [Como criar uma configuração vários SID do SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Os princípios da execução do SAP NetWeaver com base em VMs controladas por Linux no Azure. Confira [Como executar o SAP NetWeaver em VMs do Linux SUSE no Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Este guia fornece configurações específicas para Linux em VMs do Azure e os detalhes sobre como tooproperly anexar discos de armazenamento do Azure tooLinux VMs.

No momento, as VMs do Azure são certificadas pelo SAP somente para configurações de escalação vertical do SAP HANA. Ainda não há suporte para configurações de escalas horizontais de cargas de trabalho do SAP HANA. Para alta disponibilidade do SAP HANA em caso de configurações de escalação vertical, confira [Alta disponibilidade do SAP HANA em máquinas virtuais (VMs) do Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Se você estiver procurando tooget uma instância do SAP HANA ou 4HANA/S ou BW/4HANA sistema implantado em um tempo muito rápido, você deve considerar o uso de saudação do [biblioteca de dispositivo de nuvem do SAP](http://cal.sap.com). Você pode encontrar documentação sobre a implantação, por exemplo, um sistema S/4HANA por meio de SAP CAL no Azure [nesta guia](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). Você só precisa toohave é uma assinatura do Azure e um usuário SAP que possa ser registrado com a biblioteca de dispositivo de nuvem do SAP.

## <a name="additional-resources"></a>Recursos adicionais
### <a name="sap-hana-backup"></a>Backup do SAP HANA
Para obter informações sobre como fazer backup de bancos de dados do SAP HANA em VMs do Azure, confira:
* [Guia de backup para SAP HANA nas Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Backup do Azure do SAP HANA no nível do arquivo](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [Backup do SAP HANA com base em instantâneos de armazenamento](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>Biblioteca de dispositivo de nuvem do SAP
Para obter informações sobre como usar a biblioteca de dispositivo de nuvem do SAP toodeploy 4HANA/S ou BW/4HANA, consulte [4HANA/S de implantar SAP ou BW/4HANA no Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>Sistemas operacionais SAP HANA com suporte
Para obter informações sobre os sistemas operacionais com suporte SAP HANA, confira [Observação de suporte SAP nº 2235581 - SAP HANA: sistemas operacionais com suporte](https://launchpad.support.sap.com/#/notes/2235581/E). As VMs do Azure oferecem suporte a apenas um subconjunto desses sistemas operacionais. Olá seguintes sistemas operacionais são suportado toodeploy HANA SAP no Azure: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Para obter documentação SAP adicional sobre o SAP HANA e sistemas operacionais Linux diferentes, confira:

* [Observação de suporte SAP nº 171356 — software SAP no Linux: informações gerais](https://launchpad.support.sap.com/#/notes/1984787)
* [Observação de suporte SAP nº 1944799 — diretrizes SAP HANA para instalação do sistema operacional SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [Observação de suporte SAP nº 2205917 — configurações do sistema operacional recomendadas para o SAP HANA DB para SLES 12 para aplicativos SAP](https://launchpad.support.sap.com/#/notes/2205917/E)
* [Observação de suporte SAP nº 1984787 — SUSE Linux Enterprise Server 12: observações de instalação](https://launchpad.support.sap.com/#/notes/1984787)
* [Observação de suporte SAP nº 1391070 — soluções UUID do Linux](https://launchpad.support.sap.com/#/notes/1391070)
* [Observação de suporte SAP 2009879 – diretrizes SAP HANA para o sistema operacional RHEL (Red Hat Enterprise Linux)](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - Banco de dados do SAP HANA: configurações do sistema operacional recomendadas para RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>Monitoramento SAP no Azure
Para obter informações sobre o monitoramento SAP no Azure, confira:

* [Observação SAP 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). Esta observação discute o "monitoramento aprimorado" do SAP com VMs do Linux no Azure. 
* [Observação SAP 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Esta observação descreve informações sobre SAPOSCOL no Linux. 
* [Observação SAP 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Esta observação aborda as principais métricas de monitoramento para SAP no Microsoft Azure.

### <a name="azure-vm-types"></a>Tipos de VM do Azure
Os tipos de VM do Azure e os cenários de carga de trabalho com suporte do SAP no SAP HANA estão documentados nas [Plataformas de IaaS certificadas pela SAP](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

Os tipos VM do Azure que são certificados pelo SAP para o SAP NetWeaver ou Olá a camada de aplicativo 4HANA/S estão documentados em [SAP Observação 1928533 - aplicativos SAP no Azure: tipos de produtos com suporte e a VM do Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Integração do Azure do SAP-Linux tem suporte apenas em Gerenciador de recursos do Azure e não o modelo de implantação clássico hello. 

## <a name="manual-installation-of-sap-hana"></a>Instalação manual do SAP HANA
Este guia descreve como toomanually instalar HANA SAP em VMs do Azure de duas maneiras diferentes:

* Usando o SAP Software Provisioning Manager SWPM () como parte de uma instalação distribuída do NetWeaver na etapa de "instalar a instância de banco de dados" hello
* Usando Olá SAP HANA banco de dados ferramenta de Gerenciador de ciclo de vida, HDBLCM e, em seguida, instalar NetWeaver

Você também pode usar SWPM tooinstall todos os componentes (SAP HANA, servidor de aplicativos SAP hello e instância do ASCS Olá) em uma única VM, conforme descrito neste [comunicado do blog SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Essa opção não está descrita neste guia de início rápido, mas Olá problemas que você deve levar em consideração Olá mesmo.

Antes de iniciar uma instalação, é recomendável que você leia hello "Preparando Azure VMs para instalação manual do SAP HANA" seção posteriormente neste guia. Isso pode ajudar a evitar vários erros básicos que podem ocorrer quando você usa apenas uma configuração de VM do Azure padrão.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Principais etapas de instalação do SAP HANA ao usar o SAP SWPM
Esta seção lista as principais etapas de saudação de uma instalação manual, a única instância do SAP HANA ao usar a instalação do SAP SWPM tooperform um 7.5 de NetWeaver SAP distribuídas. etapas individuais da saudação são explicadas em mais detalhes nas capturas de tela neste documento.

1. Como criar uma rede virtual do Azure que inclui as duas VMs de teste.
2. Implante Olá duas VMs do Azure com os sistemas operacionais (em nosso exemplo, SUSE Linux Enterprise Server (SLES) e SLES para SAP aplicativos 12 SP1), de acordo com o modelo do Azure Resource Manager toohello.
3. Anexe dois Azure padrão ou o servidor de aplicativos de toohello para discos (por exemplo, 75 GB ou 500 GB) de armazenamento premium VM.
4. Anexe o servidor de banco de dados do HANA de toohello para discos de armazenamento premium VM. Para obter detalhes, consulte hello "Configuração de disco" seção mais adiante neste guia.
5. Dependendo dos requisitos de tamanho ou a taxa de transferência, anexar vários discos e, em seguida, criar volumes distribuídos usando o gerenciamento de volumes lógicos ou uma ferramenta de administração de vários dispositivos (MDADM) no nível de saudação SO dentro Olá VM.
6. Crie sistemas de arquivos XFS Olá anexado em discos ou volumes lógicos.
7. Monte Olá novos XFS arquivo sistemas no nível de saudação SO. Use um sistema de arquivos para todos os softwares SAP hello. Use Olá outro sistema de arquivos para o diretório de /sapmnt hello e backups, por exemplo. No servidor de banco de dados do SAP HANA hello, monte sistemas de arquivos XFS Olá nos discos de armazenamento premium Olá como /hana e /usr/sap. Esse processo é necessário tooprevent Olá sistema de arquivos raiz, que não é grande em VMs do Linux do Azure, do preenchimento.
8. Insira endereços IP locais de saudação do teste Olá VMs no arquivo hello/etc/hosts.
9. Digite hello **nofail** parâmetro hello/etc/fstab arquivo.
10. Defina parâmetros de kernel do Linux de acordo com o lançamento do sistema operacional Linux toohello que você estiver usando. Para obter mais informações, consulte Olá apropriado Observações sobre o SAP que abordam HANA e hello seção "Parâmetros do Kernel" deste guia.
11. Adicionar espaço de troca.
12. Opcionalmente, instale uma área de trabalho de gráfica no teste Olá VMs. Caso contrário, usar uma instalação remota SAPinst.
13. Baixe o software do SAP de saudação da saudação SAP Service Marketplace.
14. Instale instância do SAP ASCS Olá em VM do servidor de aplicativo hello.
15. Diretório de /sapmnt de saudação do compartilhamento entre Olá testar VMs usando NFS. Olá aplicativo servidor VM é Olá NFS.
16. Instale a instância de banco de dados hello, incluindo HANA, usando SWPM no servidor de banco de dados de saudação VM.
17. Instale o servidor de aplicativos principal de saudação (PAS) no servidor de aplicativo hello VM.
18. Inicie o Console de gerenciamento do SAP (SAP MC). Conecte-se com o SAP GUI ou HANA Studio, por exemplo.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Principais etapas de instalação do SAP HANA ao usar HDBLCM
Esta seção lista as principais etapas de saudação de uma instalação manual, a única instância do SAP HANA ao usar a instalação do SAP HDBLCM tooperform um 7.5 de NetWeaver SAP distribuídas. etapas individuais da saudação são explicadas em mais detalhes nas capturas de tela em todo este guia.

1. Como criar uma rede virtual do Azure que inclui as duas VMs de teste.
2. Implantar duas VMs do Azure com os sistemas operacionais (em nosso exemplo, SLES e SLES para SAP aplicativos 12 SP1) de acordo com o modelo do Azure Resource Manager toohello.
3. Anexe o Azure dois padrão ou o servidor de aplicativos de toohello para discos (por exemplo, 75 GB ou 500 GB) de armazenamento premium VM.
4. Anexe o servidor de banco de dados do HANA de toohello para discos de armazenamento premium VM. Para obter detalhes, consulte hello "Configuração de disco" seção mais adiante neste guia.
5. Dependendo dos requisitos de tamanho ou a taxa de transferência, anexar vários discos e criar volumes distribuídos usando o gerenciamento de volumes lógicos ou uma ferramenta de administração de vários dispositivos (MDADM) no nível de saudação SO dentro Olá VM.
6. Crie sistemas de arquivos XFS Olá anexado em discos ou volumes lógicos.
7. Monte Olá novos XFS arquivo sistemas no nível de saudação SO. Usar um sistema de arquivos para todos os softwares SAP hello e use Olá outros uma para o diretório de /sapmnt hello e backups, por exemplo. No servidor de banco de dados do SAP HANA hello, monte sistemas de arquivos XFS Olá nos discos de armazenamento premium Olá como /hana e /usr/sap. Esse processo é necessário toohelp impedir que o sistema de arquivos raiz hello, não for grande em VMs do Linux do Azure, ocupando.
8. Insira endereços IP locais de saudação do teste Olá VMs no arquivo hello/etc/hosts.
9. Digite hello **nofail** parâmetro hello/etc/fstab arquivo.
10. Definir parâmetros de kernel de acordo com o lançamento do sistema operacional Linux toohello que você estiver usando. Para obter mais informações, consulte Olá apropriado Observações sobre o SAP que abordam HANA e hello seção "Parâmetros do Kernel" deste guia.
11. Adicionar espaço de troca.
12. Opcionalmente, instale uma área de trabalho de gráfica no teste Olá VMs. Caso contrário, usar uma instalação remota SAPinst.
13. Baixe o software do SAP de saudação da saudação SAP Service Marketplace.
14. Crie um grupo, sapsys, com grupo ID 1001, no servidor de banco de dados do HANA Olá VM.
15. Instale o SAP HANA no servidor de banco de dados de saudação VM usando o Gerenciador de ciclo de vida de banco de dados de HANA (HDBLCM).
16. Instale instância do SAP ASCS Olá em VM do servidor de aplicativo hello.
17. Diretório de /sapmnt de saudação do compartilhamento entre Olá testar VMs usando NFS. Olá aplicativo servidor VM é Olá NFS.
18. Instale a instância de banco de dados hello, incluindo HANA, usando SWPM no servidor de banco de dados do HANA Olá VM.
19. Instale o servidor de aplicativos principal de saudação (PAS) no servidor de aplicativo hello VM.
20. Inicie o SAP MC. Conecte-se por meio do SAP GUI ou HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Prepare as VMs do Azure para instalação manual do SAP HANA
Esta seção aborda Olá seguintes tópicos:

* Atualizações do sistema operacional
* Configuração de disco
* Parâmetros de kernel
* Sistemas de arquivos
* arquivo Hello/etc/hosts
* Olá/etc/fstab arquivo

### <a name="os-updates"></a>Atualizações do sistema operacional
Verifique se há atualizações e correções do sistema operacional Linux antes de instalar o software adicional. Ao instalar um patch, você pode ser capaz de tooavoid uma técnica de suporte chamada toohello.

Certifique-se de que você esteja usando:
* SUSE Linux Enterprise Server para aplicativos SAP.
* Red Hat Enterprise Linux para aplicativos SAP ou Red Hat Enterprise Linux para o SAP HANA. 

Se você ainda não fez isso, registre implantação do sistema operacional Olá com sua assinatura do Linux do fornecedor de Linux hello. Observe que o SUSE tem imagens do sistema operacional para aplicativos SAP que já incluem serviços e que são registrados automaticamente.

Aqui está um exemplo de busca de patches disponíveis para SUSE Linux usando Olá **zypper** comando:

 `sudo zypper list-patches`

Dependendo do tipo de saudação do problema, os patches são classificados por categoria e severidade. Os valores usados para categoria são: **segurança**, **recomendado**, **opcional**, **recurso**, **documento** ou **yast**.
Os valores usados para gravidade são: **crítica**, **importante**, **moderada**, **baixa** ou **não especificada**.

Olá **zypper** comando procura somente para atualizações de saudação seus pacotes instalados necessário. Por exemplo, você pode usar este comando:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Você pode adicionar o parâmetro hello `--dry-run` tootest Olá atualização sem realmente atualizar sistema hello.


### <a name="disk-setup"></a>Configuração de disco
sistema de arquivos raiz Olá em uma VM do Linux no Azure tem um limite de tamanho. Portanto, é necessário tooattach em disco adicional espaço tooan VM do Azure para executar o SAP. Para o servidor de aplicativos SAP VMs do Azure, o uso de saudação de discos de armazenamento padrão do Azure pode ser suficiente. No entanto, para VMs do Azure do SAP HANA DBMS, uso de saudação de discos de armazenamento Premium do Azure para implementações de produção e não seja de produção é obrigatório.

Com base em Olá [requisitos de armazenamento do SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), Olá seguinte configuração de armazenamento Premium do Azure é sugerido: 

| SKU da VM | RAM |  hana/data e hana/log <br /> distribuídos com LVM ou MDADM | /hana/shared | /root volume | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Na configuração de disco sugeridos hello, volume de dados do HANA hello e volume de log são colocados em Olá mesmo conjunto de discos de armazenamento premium do Azure que são distribuídos com LVM ou MDADM. Não é necessário toodefine qualquer redundância RAID nível como o armazenamento Premium do Azure mantém três imagens de discos Olá para redundância. toomake-se de que você configure o armazenamento suficiente, consulte Olá [requisitos de armazenamento do SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) e [guia de atualização e instalação de servidor do SAP HANA](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Também considere volumes de taxa de transferência de outro disco rígido virtual (VHD) de saudação de Olá discos de armazenamento premium do Azure diferente conforme documentado no [Premium de alto desempenho, armazenamento e discos gerenciados para VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Você pode adicionar que mais armazenamento premium discos VMs de DBMS do HANA toohello para armazenar backups de log de transação ou de banco de dados.

Para obter mais informações sobre Olá duas ferramentas principais tooconfigure a distribuição, consulte Olá artigos a seguir:

* [Configurar RAID de software no Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configurar o LVM em uma VM Linux no Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Para obter mais informações sobre como anexar discos tooAzure VMs executando o Linux como um sistema operacional convidado, consulte [adicionar um disco tooa VM Linux](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Armazenamento Premium do Azure permite que você toodefine modos de cache de disco. Para obter Olá distribuído mantendo /hana/data e /hana/log, o cache de disco deve ser desabilitado. Para hello outros volumes (discos), Olá cache modo deve ser definido muito**ReadOnly**.

Para saber mais, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../../storage/common/storage-premium-storage.md).

modelos de JSON de exemplo toofind para criar máquinas virtuais, ir muito[modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).
modelo de vm-simples-sles Olá é um modelo básico. Ele inclui uma seção de armazenamento com um disco de dados de 100 GB adicionais. Esse modelo pode ser usado como base. Você pode adaptar a configuração específica do hello modelo tooyour.

>[!Note]
>É importante tooattach disco de armazenamento do Azure de saudação usando um UUID conforme documentado no [executando o SAP NetWeaver nas máquinas virtuais do Microsoft Azure SUSE Linux](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

No ambiente de teste hello, dois discos de armazenamento padrão do Azure foram servidor de aplicativos do SAP toohello anexado VMs, conforme mostrado no hello captura de tela a seguir. Um disco armazenados todos os softwares SAP hello (incluindo NetWeaver 7.5, a GUI do SAP e SAP HANA) para a instalação. disco segundo Olá garantiu que suficiente espaço livre está disponível para requisitos adicionais (por exemplo, dados de backup e de teste) e para Olá /sapmnt diretório (ou seja, os perfis SAP) toobe compartilhada entre todas as máquinas virtuais que pertencem a toohello estrutura SAP mesmo.

![A janela de discos do servidor de aplicativos SAP HANA exibe dois discos de dados e seus tamanhos](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Parâmetros de kernel
SAP HANA requer configurações específicas de kernel Linux, que não fazem parte de imagens de galeria do Azure padrão hello e devem ser definidas manualmente. Dependendo se você usar SUSE ou Red Hat, parâmetros de saudação podem ser diferentes. Olá Observações sobre o SAP listadas anteriormente fornecem informações sobre esses parâmetros. Nas capturas de tela hello mostradas, SUSE Linux 12 SP1 foi usado. 

SLES para GA de 12 de aplicativos SAP e SLES para SAP aplicativos 12 SP1 tem uma nova ferramenta, **adm ajustados**, que substitui o hello antigo **sapconf** ferramenta. Um perfil especial do SAP HANA está disponível para o **tuned-adm**. sistema Olá tootune SAP HANA, digite seguinte hello como um usuário raiz:

   `tuned-adm profile sap-hana`

Para obter mais informações sobre **adm ajustados**, consulte Olá [documentação SUSE sobre adm ajustados](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

Olá captura de tela a seguir, você verá como **adm ajustados** alterado Olá `transparent_hugepage` e `numa_balancing` valores, de acordo com o toohello necessárias configurações SAP HANA.

![ferramenta de adm ajustados Olá altera os valores de acordo com toorequired configurações SAP HANA](./media/hana-get-started/image005.jpg)

Usar configurações SAP HANA de kernel do hello toomake permanentes, **grub2** em 12 SLES. Para obter mais informações sobre **grub2**, vá toohello [estrutura do arquivo de configuração](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) seção Olá documentação SUSE.

Olá seguinte captura de tela mostra como Olá kernel configurações foram alteradas no arquivo de configuração de saudação e compiladas usando **grub2 mkconfig**:

![Configurações de kernel alteradas no arquivo de configuração de saudação e compilado usando grub2 mkconfig](./media/hana-get-started/image006.jpg)

Outra opção é configurações de saudação toochange usando YaST e hello **carregador de inicialização** > **parâmetros de Kernel** configurações:

![Guia de configurações de parâmetros de Kernel Olá no carregador de inicialização YaST](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Sistemas de arquivos
Olá seguinte captura de tela mostra dois sistemas de arquivos que foram criados no servidor de aplicativos SAP Olá VM sobre dois discos de armazenamento padrão do Azure anexado hello. Ambos os sistemas de arquivos são do tipo XFS e montado muito/dadosSAP e /sapsoftware.

Ele é toostructure não seja obrigatório os sistemas de arquivos dessa maneira. Você tem outras opções para estruturar o espaço em disco hello. Olá mais importante é o sistema de arquivos de raiz de saudação de tooprevent contra a falta de espaço livre.

![Dois sistemas de arquivo criados no servidor de aplicativos SAP Olá VM](./media/hana-get-started/image008.jpg)

Sobre Olá VM de banco de dados do SAP HANA, durante uma instalação do banco de dados, quando você usa SAPinst SWPM () e hello **típicos** opção de instalação, tudo o que é instalado em /hana e /usr/sap. local padrão de saudação para backup de log do SAP HANA hello está em /usr/sap. Novamente, porque se trata de sistema de arquivos importantes tooprevent Olá raiz de falta de espaço de armazenamento, certifique-se de que há espaço livre suficiente em /hana e /usr/sap antes de instalar o SAP HANA usando SWPM.

Para obter uma descrição do layout do sistema de arquivos padrão saudação do SAP HANA, consulte Olá [guia de atualização e instalação de servidor do SAP HANA](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Sistemas de arquivos adicionais criados no servidor de aplicativos SAP Olá VM](./media/hana-get-started/image009.jpg)

Quando você instala o SAP NetWeaver em SLES/SLES padrão para a imagem da Galeria do Azure 12 de aplicativos SAP, é exibida uma mensagem que diz que não há nenhum espaço de permuta, conforme mostrado no hello captura de tela a seguir. toodismiss esta mensagem, você pode adicionar manualmente um arquivo de permuta usando **dd**, **mkswap**, e **swapon**. toolearn como, procure "Adicionar um arquivo de permuta manualmente" em Olá [usando Olá YaST particionador](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) seção Olá documentação SUSE.

Outra opção é o espaço de permuta tooconfigure usando Olá agente de VM do Linux. Para obter mais informações, consulte Olá [guia do usuário do Azure Linux Agent](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Mensagem pop-up informando que não há espaço de troca suficiente](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>arquivo Hello/etc/hosts
Antes de iniciar tooinstall SAP, certifique-se de que incluir os nomes de host hello e endereços IP de saudação VMs SAP no arquivo /etc/hosts de saudação. Implantar todas as VMs do SAP hello dentro de uma rede virtual do Azure e, em seguida, use os endereços IP internos hello, conforme mostrado aqui:

![Nomes de host e endereços IP de VMs do SAP Olá listados no arquivo de /etc/hosts de saudação](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>Olá/etc/fstab arquivo

É útil tooadd Olá **nofail** arquivo do parâmetro toohello fstab. Dessa forma, se algo der errado com discos de Olá Olá VM não suspensão no processo de inicialização de saudação. Mas, lembre-se de que espaço em disco adicional pode não estar disponível e processos podem preencher o sistema de arquivos raiz hello. Se /hana estiver ausente, o SAP HANA não será iniciado.

![Adicionar Olá nofail parâmetro toohello fstab arquivo](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Área de trabalho GNOME gráfica no SLES 12/SLES para Aplicativos SAP 12
Esta seção aborda Olá seguintes tópicos:

* A instalação de área de trabalho do hello GNOME e xrdp em SLES 12/SLES para 12 de aplicativos SAP
* Execução do SAP MC baseado em Java usando o Firefox no SLES 12/SLES para aplicativos SAP 12

Você também pode usar alternativas, como Xterminal ou VNC (não descritos nesta guia).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>A instalação de área de trabalho do hello GNOME e xrdp em SLES 12/SLES para 12 de aplicativos SAP
Se você tiver um plano de fundo do Windows, pode facilmente usar uma área de trabalho gráfica diretamente dentro de saudação VMs do Linux SAP toorun Firefox, SAPinst, SAP GUI, SAP MC ou HANA Studio e conectar toohello VM por meio de saudação protocolo de área de trabalho remota (RDP) de um computador com Windows. Interfaces gráficas do usuário depende de políticas de sua empresa sobre como adicionar os sistemas baseados em Linux tooproduction e não seja de produção, você pode querer tooinstall GNOME em seu servidor. tooinstall Olá GNOME área de trabalho em um SLES/12 SLES do Azure para SAP aplicativos 12 VM:

1. Instale área de trabalho do hello GNOME inserindo Olá comando (por exemplo, em uma janela PuTTY) a seguir:

   `zypper in -t pattern gnome-basic`

2. Instale xrdp tooallow toohello uma conexão VM por meio de RDP:

   `zypper in xrdp`

3. Edite /etc/sysconfig/windowmanager e defina o saudação padrão janela Gerenciador tooGNOME:

   `DEFAULT_WM="gnome"`

4. Executar **comando chkconfig** toomake-se de que xrdp inicia automaticamente após a reinicialização:

   `chkconfig -level 3 xrdp on`

5. Se você tiver um problema com hello conexão RDP, tente toorestart (em uma janela PuTTY, por exemplo):

   `/etc/xrdp/xrdp.sh restart`

6. Se uma reinicialização xrdp mencionado Olá anterior etapa não funcionar, procure um arquivo .pid:

   `check /var/run` 

   Procure `xrdp.pid`. Se você achar, removê-lo e tente toorestart novamente.

### <a name="starting-sap-mc"></a>Inicialização do SAP MC
Depois de instalar a área de trabalho GNOME Olá, iniciando Olá gráfica baseada em Java MC do SAP do Firefox durante a execução em um Azure SLES 12/SLES de VM de 12 de aplicativos SAP pode exibir um erro devido a saudação ausente plug-in de navegador Java.

saudação de toostart URL Olá MC SAP é `<server>:5<instance_number>13`.

Para obter mais informações, consulte [saudação inicial Console de gerenciamento baseado na Web do SAP](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Olá, seguinte captura de tela mostra Olá mensagem de erro que é exibida quando Olá plug-in de navegador Java está ausente:

![Mensagem de erro indicando a falta do plug-in de navegador Java](./media/hana-get-started/image013.jpg)

Problema de saudação toosolve unidirecional é Olá tooinstall ausente plug-in usando YaST, conforme mostrado no hello captura de tela a seguir:

![Usando tooinstall YaST ausente plug-in](./media/hana-get-started/image014.jpg)

Quando você insere novamente Olá SAP URL do Console de gerenciamento, será exibida uma mensagem perguntando você tooactivate Olá plug-in:

![Caixa de diálogo solicitando a ativação do plug-in](./media/hana-get-started/image015.jpg)

Você também poderá receber uma mensagem de erro sobre um arquivo ausente, javafx.properties. Este é o requisito de toohello relacionados da Oracle Java 1.8 para SAP GUI 7.4. (Confira [Observação SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Olá versão IBM Java nem a pacote de openjdk Olá entregues com SLES/SLES para 12 de aplicativos SAP inclui o arquivo de javafx.properties necessário hello. solução de saudação é toodownload e instale o Java SE 8 do Oracle.

Para obter informações sobre um problema semelhante com openjdk openSUSE, consulte o segmento de discussão Olá [Leap SAPGui 7.4 Java para openSUSE 42.1](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Instalação manual do SAP HANA: SWPM
série de saudação de capturas de tela nesta seção mostra principais etapas Olá para instalar 7.5 do SAP NetWeaver e SAP HANA SP12 quando você usar SWPM (SAPinst). Como parte de uma instalação NetWeaver 7.5, SWPM também pode instalar o banco de dados do hello HANA como uma única instância.

Em um ambiente de teste de exemplo, instalamos apenas um servidor de aplicativos do Advanced Business Application Programming (ABAP). Conforme mostrado na Olá captura de tela a seguir, usamos Olá **sistema distribuído** opção tooinstall Olá ASCS e instâncias de servidor de aplicativo principal em uma VM do Azure e SAP HANA como sistema de banco de dados de saudação em outra VM do Azure.

![ASCS e instâncias de servidor de aplicativo principal instaladas usando a opção de sistema distribuído Olá](./media/hana-get-started/image012.jpg)

Após a instância do ASCS hello está instalada na VM do servidor de aplicativo hello e está definido muito "verde" no hello Console de gerenciamento do SAP (mostrado Olá captura de tela a seguir), Olá /sapmnt diretório (incluindo o diretório de perfil do SAP Olá) deve ser compartilhado com VM do servidor de banco de dados do SAP HANA hello. etapa de instalação Olá DB precisa acessar as informações de toothis. acesso de tooprovide de maneira melhor Olá é toouse NFS, que pode ser configurado usando YaST.

![Instância do SAP Console de gerenciamento mostrando Olá ASCS instalado na VM do servidor de aplicativo hello e defina muito "verde"](./media/hana-get-started/image016.jpg)

No servidor de aplicativo hello VM, Olá/diretório sapmnt deve ser compartilhado por meio de NFS usando Olá **rw** e **no_root_squash** opções. Olá padrões são **ro** e **root_squash**, que pode levar tooproblems quando você instalar a instância de banco de dados de saudação.

![Compartilhar o diretório de /sapmnt de saudação via NFS usando as opções de rw e no_root_squash Olá](./media/hana-get-started/image017b.jpg)

Como mostra a próxima captura de tela de hello, Olá /sapmnt compartilhamento do servidor de aplicativo hello VM deve ser configurado no servidor de banco de dados do SAP HANA Olá VM usando **cliente NFS** (e YaST).

![compartilhamento de /sapmnt de saudação configurado usando o cliente NFS](./media/hana-get-started/image018b.jpg)

instalação de tooperform um 7.5 NetWeaver distribuído (**instância de banco de dados**), como Olá mostrado na captura de tela a seguir, inscrever-se na VM do servidor de banco de dados do SAP HANA toohello e iniciar SWPM.

![Instalar uma instância de banco de dados de assinatura na VM do servidor de banco de dados do SAP HANA toohello e iniciando SWPM](./media/hana-get-started/image019.jpg)

Depois de selecionar **típicos** instalação e a mídia de instalação toohello do caminho hello, insira um SID de banco de dados, nome de host hello, número da instância hello e senha de administrador de sistema Olá banco de dados.

![página Olá SAP HANA banco de dados sistema administrador entrar](./media/hana-get-started/image035b.jpg)

Insira a senha de saudação para esquema DBACOCKPIT hello:

![caixa de entrada de senha Olá para o esquema DBACOCKPIT Olá](./media/hana-get-started/image036b.jpg)

Digite uma pergunta de senha de esquema SAPABAP1 hello:

![Digite uma pergunta de senha de esquema SAPABAP1 Olá](./media/hana-get-started/image037b.jpg)

Após a conclusão de cada tarefa, uma marca de seleção verde é exibida próxima fase tooeach de saudação processo de instalação do banco de dados. mensagem de saudação "execução de... Instância de banco de dados foi concluída".

![Janela de tarefa concluída com mensagem de confirmação](./media/hana-get-started/image023.jpg)

Após a instalação bem-sucedida, Olá Console de gerenciamento do SAP também deve mostrar Olá instância de banco de dados como "green" e exibir a lista completa de saudação de processos do SAP HANA (hdbindexserver, hdbcompileserver e assim por diante).

![Janela do SAP Management Console com lista de processos do SAP HANA](./media/hana-get-started/image024.jpg)

Olá, seguinte captura de tela mostra Olá partes da estrutura de arquivo hello no diretório de /hana/shared de saudação SWPM criado durante a saudação instalação HANA. Como não há nenhuma opção toospecify um caminho diferente, é importante toomount espaço em disco adicional no diretório de /hana Olá antes Olá instalação SAP HANA usando SWPM. Isso impede que o sistema de arquivos raiz Olá da falta de espaço livre.

![estrutura de arquivo Hello /hana/shared diretório criada durante a instalação do HANA](./media/hana-get-started/image025.jpg)

Esta captura de tela mostra a estrutura de arquivo de saudação do diretório de /usr/sap hello:

![estrutura do arquivo Hello /usr/sap diretório](./media/hana-get-started/image026.jpg)

Olá última etapa da instalação de ABAP Olá distribuído é instância de servidor de aplicativo principal tooinstall hello:

![Instância de servidor de aplicativo principal ABAP instalação mostrando como etapa final Olá](./media/hana-get-started/image027b.jpg)

Após a instalação instância de servidor de aplicativo principal hello e SAP GUI, usar Olá **DBA Cockpit** tooconfirm de transação que Olá instalação SAP HANA foi concluída corretamente:

![Janela DBA Cockpit confirmando a instalação bem-sucedida](./media/hana-get-started/image028b.jpg)

Como uma etapa final, você pode deseja instalar toofirst HANA Studio no servidor de aplicativos SAP Olá VM e, em seguida, conecte-se a instância de SAP HANA de toohello que está em execução no servidor de banco de dados de saudação VM:

![Instalar o SAP HANA Studio no servidor de aplicativos SAP Olá VM](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Instalação manual do SAP HANA: HDBLCM
Em adição tooinstalling SAP HANA como parte de uma instalação distribuída usando SWPM, você pode instalar pela primeira vez, Olá HANA autônomo usando HDBLCM. Em seguida, você pode instalar o SAP NetWeaver 7.5, por exemplo. capturas de tela de saudação nesta seção mostram como esse processo funciona.

Para obter mais informações sobre Olá ferramenta HANA HDBLCM, consulte:

* [Olá escolhendo correto SAP HANA HDBLCM para sua tarefa](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools (Ferramentas de gerenciamento de ciclo de vida do SAP HANA)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide (Guia de instalação e atualização do servidor SAP HANA)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

configuração de ID de saudação do grupo de tooavoid problemas com um padrão `\<HANA SID\>adm user` (criado pela ferramenta HDBLCM Olá), definir um novo grupo chamado `sapsys` usando a ID do grupo `1001` antes de instalar o SAP HANA via HDBLCM:

![Grupo novo "sapsys" definido usando a ID de grupo 1001](./media/hana-get-started/image030.jpg)

Quando você inicia Olá HDBLCM pela primeira vez, é exibido um menu Iniciar simples. Selecionar item 1, **instalar o novo sistema**, conforme mostrado no hello captura de tela a seguir:

![Opção "Instalar o novo sistema" na janela de início HDBLCM Olá](./media/hana-get-started/image031.jpg)

Olá seguinte captura de tela exibe todas as opções de chave de saudação que você selecionou anteriormente.

> [!IMPORTANT]
> Os diretórios que são nomeados para o log do HANA e volumes de dados, bem como caminho de instalação da saudação (hana/compartilhado neste exemplo) e /usr/sap, não devem ser parte do sistema de arquivos raiz hello. Esses diretórios pertencem toohello discos de dados do Azure que estavam anexado toohello VM (descrito na seção hello "configuração de disco"). Essa abordagem ajuda a impedir que o sistema de arquivos raiz Olá ficar sem espaço. Olá captura de tela a seguir, você pode ver esse administrador de sistema do HANA Olá tem a ID de usuário `1005` e faz parte da saudação `sapsys` grupo (ID `1001`) que foi definida antes da instalação de saudação.

![Lista de todos os principais componentes do SAP HANA selecionados anteriormente](./media/hana-get-started/image032.jpg)

Você pode verificar Olá `\<HANA SID\>adm user` (`azdadm` em Olá captura de tela a seguir) no Olá/etc/senha directory:

![HANA \<HANA SID\>detalhes do usuário adm listado no diretório de senhas do hello/etc /](./media/hana-get-started/image033.jpg)

Depois de instalar o SAP HANA usando HDBLCM, você pode ver estrutura do arquivo hello no Studio do HANA SAP, conforme mostrado no hello captura de tela a seguir. esquema de SAPABAP1 Hello, que inclui todas as tabelas de SAP NetWeaver hello, ainda não está disponível.

![Estrutura de arquivos do SAP HANA no SAP HANA Studio](./media/hana-get-started/image034.jpg)

Após a instalação do SAP HANA, você poderá instalar o SAP NetWeaver nele. Como Olá mostrado na captura de tela a seguir, instalação de saudação foi executada como uma instalação distribuída usando SWPM (conforme descrito na seção anterior Olá). Quando você instala a instância de banco de dados de saudação usando SWPM, você insere Olá mesmos dados usando HDBLCM (por exemplo, nome de host, HANA SID e o número de instância). SWPM, em seguida, usa a instalação do HANA existente hello e adiciona mais esquemas.

![Uma instalação distribuída realizada pelo SWPM](./media/hana-get-started/image035b.jpg)

Olá seguinte captura de tela mostra Olá SWPM instalação etapa em que você inserir dados sobre o esquema DBACOCKPIT hello:

![etapa de instalação SWPM Olá onde os dados de esquema DBACOCKPIT são inseridos](./media/hana-get-started/image036b.jpg)

Inserir dados sobre o esquema de SAPABAP1 hello:

![Inserindo dados sobre o esquema de SAPABAP1 Olá](./media/hana-get-started/image037b.jpg)

Após Olá instalação SWPM de instância de banco de dados, você pode ver o esquema SAPABAP1 Olá SAP HANA Studio:

![esquema de saudação SAPABAP1 no Studio do SAP HANA](./media/hana-get-started/image038b.jpg)

Por fim, depois que o servidor de aplicativos SAP hello e instalações de GUI do SAP são concluídas, você pode verificar instância de banco de dados do HANA hello usando Olá **DBA Cockpit** transação:

![instância de banco de dados do HANA Olá verificada com hello transação Cockpit DBA](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Downloads de software SAP
Você pode baixar o software de saudação SAP Service Marketplace, conforme mostrado no hello capturas de tela a seguir.

Baixar o NetWeaver 7.5 para Linux/HANA:

 ![Janela Instalação e Atualização do Serviço SAP para baixar o NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Baixar o HANA SP12 Platform Edition:

 ![Janela Instalação e Atualização do Serviço SAP para baixar o HANA SP12 Platform Edition](./media/hana-get-started/image002.jpg)

