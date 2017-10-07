---
title: "aaaTesting SAP NetWeaver nas máquinas virtuais do Microsoft Azure SUSE Linux | Microsoft Docs"
description: Testando o SAP NetWeaver em VMs SUSE Linux no Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Executando o SAP NetWeaver em VMs do SUSE Linux no Microsoft Azure
Este artigo descreve vários tooconsider de coisas quando você estiver executando o SAP NetWeaver nas máquinas virtuais de SUSE Linux do Microsoft Azure (VMs). A partir de 19 de maio de 2016, o SAP NetWeaver tem suporte oficial em VMs do SUSE Linux no Azure. Todos os detalhes relativos a versões do Linux, versões de kernel do SAP e assim por diante podem ser encontrados na nota do SAP 1928533 "Aplicativos SAP no Azure: produtos com suporte e tipos de VM do Azure".
Mais documentação sobre o SAP em VMs Linux podem ser encontrados aqui: [Usando o SAP em VMs (máquinas virtuais) do Linux](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Olá informações a seguir deve ajudar a evitar armadilhas em potencial.

## <a name="suse-images-on-azure-for-running-sap"></a>Imagens do SUSE no Azure para executar o SAP
Para executar o SAP NetWeaver no Azure, use apenas o SUSE Linux Enterprise Server SLES 12 ( SPx ) - consulte também nota do SAP 1928533. Uma imagem SUSE especial é em hello Azure Marketplace ("SLES 11 SP3 para SAP CAL"), mas isso não é destinado para uso geral. Não use esta imagem porque ele está reservado para Olá [biblioteca de dispositivo de nuvem do SAP](https://cal.sap.com/) solução.  

Use o Azure Resource Manager para todos os novos testes e instalações no Azure. toolook para imagens do SUSE SLES e versões usando o Azure PowerShell ou hello Azure interface de linha de comando (CLI), use Olá comandos a seguir. Você pode usar Olá saída, por exemplo, toodefine Olá imagem do sistema operacional em um modelo JSON para implantar uma nova VM Linux SUSE.
Estes comandos do PowerShell são válidos para a versão do Azure PowerShell 1.0.1 e posteriores.

Embora seja possível toouse Olá SLES imagens padrão para instalações do SAP é recomendável toomake uso de Olá SLES novo para imagens do SAP que estão disponíveis agora no hello Azure Galeria de imagem. Mais informações sobre essas imagens podem ser encontradas em Olá correspondente [página Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) ou hello [página da web de perguntas frequentes sobre o SUSE sobre SLES para SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Procure por editores existentes, incluindo o SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Procure por ofertas existentes do SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Procure por ofertas do SLES SUSE:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Procure por uma versão específica do SKU do SLES:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Instalando o WALinuxAgent em uma VM SUSE
Agente de saudação chamado WALinuxAgent é parte de imagens SLES Olá Olá Azure Marketplace. Para saber mais sobre como instalá-lo manualmente (por exemplo, ao carregar um VHD (disco rígido virtual) do sistema operacional SLES no local), confira:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [As tabelas](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>"Monitoramento avançado" do SAP
SAP "monitoramento avançado" é um toorun pré-requisitos obrigatório SAP no Azure. Verifique os detalhes na nota do SAP 2191498 "SAP no Linux com o Azure: monitoramento aprimorado".

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Anexar discos de dados do Azure tooan VM do Linux do Azure
Você nunca deve montar tooan de discos de dados do Azure VM do Linux do Azure usando a ID do dispositivo hello. Em vez disso, use o identificador universalmente exclusivo da saudação (UUID). Tenha cuidado ao usar discos de dados do Azure de toomount ferramentas gráficas, por exemplo. Verifique as entradas Olá /etc/fstab.

problema Olá Olá ID do dispositivo é que ele pode ser alterado e, em seguida, Olá VM do Azure pode travar no processo de inicialização de saudação. problema de saudação toomitigate, você pode adicionar parâmetro de nofail hello em /etc/fstab. No entanto, tenha cuidado com nofail porque os aplicativos podem usar o ponto de montagem hello como antes e podem gravar no sistema de arquivos raiz Olá no caso de um disco de dados do Azure externos não foi montado durante a inicialização de saudação.

Olá única exceção toomounting via UUID é anexar um disco do sistema operacional para solução de problemas, conforme descrito em Olá seção a seguir.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Solução de problemas de uma VM SUSE que não está mais acessível
Pode haver situações em que uma VM SUSE no Azure trava no processo de inicialização da saudação (por exemplo, com um erro relacionado ao montar os discos). Você pode verificar esse problema usando o recurso de diagnóstico de inicialização Olá para máquinas virtuais do Azure v2 no hello portal do Azure. Para saber mais, consulte [Diagnóstico de inicialização](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Problema de saudação toosolve unidirecional é tooattach disco do sistema operacional de saudação do hello danificado VM tooanother SUSE VM no Azure. Faça as alterações apropriadas como /etc/fstab de editar ou remover regras de udev de rede, conforme descrito na próxima seção, Olá.

Há um tooconsider de importante. Implantando várias VMs SUSE da saudação a mesma imagem do Marketplace do Azure (por exemplo, SLES 11 SP4) faz com que Olá SO tooalways disco ser montados por Olá mesmo UUID. Portanto, usando Olá UUID tooattach um disco do sistema operacional de uma VM diferente que foi implantado usando Olá a mesma imagem do Azure Marketplace resultará em dois UUIDs idênticos. Isso causa problemas e pode significar que Olá VM destinam-se para a solução de problemas na verdade inicializará a partir Olá anexado e danificado disco do sistema operacional, em vez de Olá original.

Há dois tooavoid de maneiras isso:

* Use uma imagem diferente do Azure Marketplace para Olá VM (por exemplo, SLES 11 SPx, em vez de 12 SLES) de solução de problemas.
* Não anexar o disco do sistema operacional Olá danificado de outra VM usando o UUID – use algo mais.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Carregar uma VM SUSE de tooAzure local
Para obter uma descrição de tooupload de etapas de saudação uma VM SUSE de tooAzure local, consulte [preparar uma máquina virtual SLES ou openSUSE para o Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Se você quiser tooupload uma VM sem desprovisionamento Olá etapa final hello (por exemplo, tookeep uma instalação existente do SAP, bem como o nome de host Olá), verifique Olá itens a seguir:

* Verifique se que esse disco Olá SO está montado usando o UUID e não hello identificação do dispositivo. Alterar tooUUID just-in /etc/fstab não é suficiente para o disco do sistema operacional hello. Além disso, não se esqueça de carregador de inicialização de saudação tooadapt usando YaST ou editando /boot/grub/menu.lst.
* Se você usar o formato VHDX de saudação para disco do sistema operacional do SUSE hello e convertê-la tooVHD para carregar tooAzure, é muito provável que esse dispositivo de rede Olá deixará de ser eth0 tooeth1. tooavoid problemas quando você estiver inicializando no Azure posteriormente, alterar tooeth0 back conforme descrito em [corrigir eth0 em clonado SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Além toowhat descrito no artigo de hello, recomendamos que você remova este:

   /lib/udev/rules.d/75-persistent-net-generator.rules

Você também pode instalar hello Azure Linux Agent (waagent) toohelp evitar possíveis problemas, como não há várias NICs.

## <a name="deploying-a-suse-vm-on-azure"></a>Implantando uma VM SUSE no Azure
Você deve criar novas VMs SUSE usando arquivos de modelo JSON no novo modelo de Gerenciador de recursos do Azure hello. Depois que o arquivo de modelo Olá JSON é criado, você pode implantar Olá VM usando Olá CLI comando como uma alternativa tooPowerShell a seguir:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Para obter mais detalhes sobre os arquivos de modelo JSON, veja [Criação de modelos do Azure Resource Manager](../../../resource-group-authoring-templates.md) e [Modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).

Para obter mais detalhes sobre CLI e Gerenciador de recursos do Azure, consulte [Olá Use CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Chave de licença e hardware do SAP
Para certificação Olá oficial do Azure do SAP um novo mecanismo foi introduzido toocalculate Olá SAP chave de hardware que é usado para a licença do SAP hello. kernel do SAP Olá tinha toobe adaptado toomake use isso. As versões anteriores de kernel do SAP para Linux não incluíam essa alteração de código. Portanto, em certas situações (por exemplo, a VM do Azure redimensionamento), alterar a chave de hardware Olá SAP e licenças SAP Olá foi deixará de ser válido. Isso é resolvido no kernels de Linux SAP mais recentes hello. Para obter detalhes, consulte nota do SAP 1928533.

## <a name="suse-sapconf-package--tuned-adm"></a>SUSE sapconf package / tuned-adm
O SUSE fornece um pacote chamado "sapconf", que gerencia um conjunto de configurações específicas do SAP. Para obter mais detalhes sobre quais este pacote faz e como tooinstall e usá-lo, consulte [usando sapconf tooprepare um sistemas SAP do SUSE Linux Enterprise Server toorun](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) e [novidades sapconf ou como tooprepare um SUSE Linux Enterprise Servidor para execução de sistemas SAP? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

No hello enquanto há uma nova ferramenta que substitui sapconf - ADM ajustadas. Um pode encontrar mais detalhes sobre essa ferramenta Olá dois links abaixo a seguir.

A documentação do SLES sobre tuned-adm profile sap-hana pode ser encontrada [aqui](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Ajustes de sistemas para cargas de trabalho do SAP com tuned-adm - podem ser encontrados [aqui](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) no capítulo 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>Compartilhamento de NFS em instalações SAP distribuídas
Se você tiver uma instalação distribuída – por exemplo, em que você deseja que o banco de dados do tooinstall hello e Olá servidores de aplicativos SAP em VMs separadas: você pode compartilhar diretório /sapmnt de saudação por meio de sistema de arquivo de rede (NFS). Se você tiver problemas com as etapas de instalação Olá depois de criar Olá para /sapmnt de compartilhamento NFS, verifique toosee se "no_root_squash" for definida para o compartilhamento de saudação.

## <a name="logical-volumes"></a>Volumes lógicos
Em Olá anterior se um necessário um grande volume lógico em vários discos de dados do Azure (por exemplo, para Olá banco de dados SAP), era recomendado toouse mdadm como lvm não foi totalmente validada ainda no Azure. toolearn como tooset RAID de Linux no Azure usando mdadm, consulte [configurar software RAID no Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No hello enquanto isso partir do início de maio de 2016 também lvm tem suporte total no Azure e pode ser usado como uma alternativa toomdadm. Para obter informações adicionais sobre o lvm no Azure, veja [Configurar o LVM em uma VM do Linux no Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Repositório SUSE do Azure
Se você tiver um problema com o repositório do acesso toohello padrão SUSE do Azure, você pode usar um comando simples tooreset-lo. Isso pode ocorrer se você criar uma imagem do sistema operacional privada em uma região do Azure e cópia Olá imagem tooa diferentes região onde você deseja toodeploy novas VMs com base nesta imagem privada do sistema operacional. Olá comando dentro de saudação VM a seguir, basta execute:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Área de trabalho Gnome
Se quiser que toouse Olá Gnome desktop tooinstall um sistema completo de demonstração SAP em uma única VM – incluindo uma SAP GUI, navegador e o console de gerenciamento do SAP-- usam essa dica tooinstall em imagens do Azure SLES hello:

   Para o SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Para o SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Suporte do SAP para Oracle no Linux em nuvem Olá
Há uma restrição de suporte da Oracle para Linux em ambientes virtualizados. Embora isso não é um tópico específico do Azure, é importante toounderstand. O SAP não oferece suporte ao Oracle no SUSE ou ao Red Hat em uma nuvem pública como o Azure. toodiscuss neste tópico, entre em contato diretamente com Oracle.

