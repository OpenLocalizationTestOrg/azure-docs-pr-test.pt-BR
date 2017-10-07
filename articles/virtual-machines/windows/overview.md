---
title: "Visão geral de máquinas virtuais de aaaWindows | Microsoft Docs"
description: "Saiba mais sobre como criar e gerenciar máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Visão geral das máquinas virtuais do Windows no Azure

VM (Máquinas Virtuais) do Azure é um dos vários tipos de [recursos de computação sob demanda escalonáveis](../../app-service-web/choose-web-site-cloud-service-vm.md) oferecidos pelo Azure. Normalmente, você escolher uma VM quando precisar de mais controle sobre o ambiente de computação de saudação do hello outras opções oferecem. Este artigo fornece informações sobre o que você deve considerar antes de criar uma VM, como criá-la e como gerenciá-la.

Fornece uma VM do Azure Olá flexibilidade da virtualização sem a necessidade de toobuy e manter o hardware físico Olá que o executa. No entanto, você ainda precisa toomaintain Olá VM executando tarefas, como configurar, corrigir e instalar software de saudação que será executado nele.

Máquinas virtuais do Azure podem ser usadas de várias maneiras. Alguns exemplos incluem:

* **Desenvolvimento e teste** – VMs do Azure oferecem uma rápida e fácil maneira toocreate um computador com configurações específicas necessárias toocode e testar um aplicativo.
* **Aplicativos em nuvem Olá** – porque a demanda para o seu aplicativo pode flutuar, pode fazer sentido, financeiramente falando toorun-lo em uma máquina virtual no Azure. Você paga por VMs extras quando precisa delas e as desliga quando não são necessárias.
* **Estendido datacenter** – máquinas virtuais em uma rede virtual do Azure podem ser facilmente a rede da organização tooyour conectado.

saudação de VMs que seu aplicativo usa pode escalar verticalmente e toowhatever está toomeet necessária às suas necessidades.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>O que é necessário toothink sobre antes de criar uma máquina virtual?
Sempre há uma infinidade de [considerações de design](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) quando você cria uma infraestrutura de aplicativo no Azure. Esses aspectos de uma VM são toothink importante sobre antes de começar:

* nomes de saudação recursos do aplicativo
* local de Olá onde os recursos de saudação são armazenados
* tamanho de saudação do hello VM
* número máximo de saudação de máquinas virtuais que podem ser criados
* executa o sistema operacional Olá Olá VM
* configuração de saudação do hello VM após ele ser iniciado
* Olá que Olá que VM precisa de recursos relacionados

### <a name="naming"></a>Nomenclatura
Uma máquina virtual tem um [nome](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooit atribuído e é necessário um nome de computador configurado como parte do sistema operacional de saudação. nome de saudação de uma VM pode ser too15 caracteres.

Se você usar o disco do sistema operacional Azure toocreate Olá, nome do computador hello e nome da máquina virtual Olá Olá mesmo. Se você [carregar e usar sua própria imagem](upload-generalized-managed.md) que contém um sistema operacional configurado anteriormente e usá-lo toocreate uma máquina virtual, os nomes de saudação podem ser diferentes. É recomendável que, quando você carrega seu próprio arquivo de imagem, você faça nome do computador Olá no sistema operacional de saudação e nome da máquina virtual Olá Olá mesmo.

### <a name="locations"></a>Locais
Todos os recursos criados no Azure são distribuídos em vários [regiões geográficas](https://azure.microsoft.com/regions/) em torno de Olá, mundo. Geralmente, é chamado de região Olá **local** quando você cria uma máquina virtual. Para uma VM local Olá Especifica onde Olá os discos rígidos virtuais são armazenados.

Esta tabela mostra algumas das maneiras de saudação, que você pode obter uma lista de locais disponíveis.

| Método | Descrição |
| --- | --- |
| Portal do Azure |Selecione um local na lista de hello quando você cria uma máquina virtual. |
| Azure PowerShell |Saudação de uso [AzureRmLocation Get](/powershell/module/azurerm.resources/get-azurermlocation) comando. |
| API REST |Saudação de uso [listar locais](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) operação. |

### <a name="vm-size"></a>Tamanho da VM
Olá [tamanho](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) de saudação VM que você usa é determinado pela carga de trabalho de saudação que você deseja toorun. tamanho Olá que você escolher determinará fatores como a capacidade de armazenamento, memória e potência de processamento. O Azure oferece uma ampla variedade de tamanhos toosupport muitos tipos de uso.

O Azure cobra um [preço por hora](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) com base no tamanho da VM hello e o sistema operacional. Para horas parciais, Azure cobra apenas pelos minutos Olá usados. O armazenamento terá o preço e será cobrado separadamente.

### <a name="vm-limits"></a>Limites de VM
Sua assinatura possui padrão [limites de cota](../../azure-subscription-service-limits.md) que podem afetar a implantação de saudação de várias VMs para seu projeto. o limite atual de saudação em uma base por assinatura é 20 VMs por região. Os limites podem ser aumentados preenchendo um tíquete de suporte para solicitar um aumento.

### <a name="operating-system-disks-and-images"></a>Imagens e discos de sistema operacional
Máquinas virtuais usam [discos rígidos virtuais (VHDs)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore seu sistema operacional (SO) e os dados. VHDs também são usados para imagens de saudação, que você pode escolher entre tooinstall um sistema operacional. 

O Azure fornece muitos [imagens marketplace](https://azure.microsoft.com/marketplace/virtual-machines/) toouse com várias versões e tipos de sistemas operacionais Windows Server. As imagens do Marketplace são identificadas por editor de imagem, oferta, sku e versão (normalmente, a versão é especificada como a versão mais recente). 

Esta tabela mostra algumas maneiras que você pode encontrar informações de saudação de uma imagem.

| Método | Descrição |
| --- | --- |
| Portal do Azure |valores Hello são especificados automaticamente para você quando você seleciona uma imagem toouse. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -local "local"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -local "local"-"publisherName" do editor<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "location" -Publisher "publisherName" -Offer "offerName" |
| APIs REST |[Listar editores de imagem](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Listar ofertas de imagem](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Listar skus de imagem](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

Você pode escolher muito[carregar e usar sua própria imagem](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) e quando você fizer isso, o nome do publicador hello, oferta e sku não são usados.

### <a name="extensions"></a>Extensões
As [extensões](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) de VM dão à VM recursos adicionais por meio de configuração pós-implantação e tarefas automatizadas.

Estas tarefas comuns podem ser realizadas usando extensões:

* **Executar scripts personalizados** – hello [extensão personalizada de Script](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ajuda você a configurar as cargas de trabalho em Olá VM executando o script quando hello VM é provisionada.
* **Implantar e gerenciar configurações de** – hello [extensão de configuração de estado de desejado (DSC) do PowerShell](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ajuda você a configurar DSC em uma VM toomanage ambientes e configurações.
* **Coletar dados de diagnóstico** – hello [extensão de diagnóstico do Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ajuda você a configurar Olá VM toocollect dados de diagnóstico que podem ser usado toomonitor Olá integridade de seu aplicativo.

### <a name="related-resources"></a>Recursos relacionados
Olá recursos nesta tabela são usados por Olá VM precisam tooexist ou e ser criados quando Olá VM é criada.

| Recurso | Obrigatório | Descrição |
| --- | --- | --- |
| [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md) |Sim |Olá VM deve estar contido em um grupo de recursos. |
| [Conta de armazenamento](../../storage/common/storage-create-storage-account.md) |Sim |Olá VM precisa Olá toostore de conta de armazenamento de seus discos rígidos virtuais. |
| [Rede virtual](../../virtual-network/virtual-networks-overview.md) |Sim |Olá VM deve ser um membro de uma rede virtual. |
| [Endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Não |Olá VM pode ter um tooit tooremotely público do IP endereço atribuído a acessá-lo. |
| [Interface de rede](../../virtual-network/virtual-network-network-interface.md) |Sim |Olá VM precisa Olá toocommunicate de interface de rede na rede de saudação. |
| [Discos de dados](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Não |Olá VM pode incluir recursos de armazenamento de tooexpand de discos de dados. |

## <a name="how-do-i-create-my-first-vm"></a>Como criar minha primeira VM?
Você tem várias opções para criar a VM. opção Olá que você escolher depende do ambiente Olá em que estão. 

Esta tabela fornece informações tooget que começou a criar sua VM.

| Método | Artigo |
| --- | --- |
| Portal do Azure |[Criar uma máquina virtual que executa o Windows usando o portal de saudação](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Modelos |[Criar uma máquina virtual do Windows com um modelo do Gerenciador de Recursos](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Criar uma VM do Windows usando o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| SDKs do cliente |[Implantar recursos do Azure usando C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| APIs REST |[Criar ou atualizar uma VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

Você espera que isso nunca aconteça, mas ocasionalmente algo dá errado. Se isso ocorrer tooyou, examinar as informações sobre a saudação em [problemas de implantação do Gerenciador de recursos de solução de problemas com a criação de uma máquina virtual Windows no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Como gerenciar o hello VM que criei?
As VMs podem ser gerenciadas usando um portal baseado em navegador, ferramentas de linha de comando com suporte para scripts ou diretamente por meio de APIs. Algumas tarefas típicas de gerenciamento que você pode realizar estão obtendo informações sobre uma VM, logon tooa VM, gerenciar a disponibilidade e a realização de backups.

### <a name="get-information-about-a-vm"></a>Obter informações sobre uma VM
Esta tabela mostra algumas das maneiras de saudação que você pode obter informações sobre uma máquina virtual.

| Método | Descrição |
| --- | --- |
| Portal do Azure |No menu de hub hello, clique em **máquinas virtuais** e, em seguida, selecione Olá VM na lista de saudação. Na folha de saudação para Olá VM, você tem acesso toooverview informações, os valores de configuração e métricas de monitoramentos. |
| Azure PowerShell |Para obter informações sobre como usar o PowerShell toomanage VMs, consulte [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| API REST |Saudação de uso [informações obter VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) informações de tooget operação sobre uma máquina virtual. |
| SDKs do cliente |Para obter informações sobre como usar c# toomanage VMs, consulte [gerenciar máquinas virtuais do Azure usando o Gerenciador de recursos do Azure e c#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Faça logon no toohello VM
Use Olá botão de conectar no portal do Azure de saudação muito[iniciar uma sessão de área de trabalho remota (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pode, às vezes, dar errado durante a tentativa de toouse uma conexão remota. Se essa situação ocorrer tooyou, verifique informações de ajuda de saudação em [tooan de conexões de área de trabalho remota solucionar problemas do Azure máquina virtual que executa o Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Gerenciar disponibilidade
É importante que você toounderstand como muito[garantir a alta disponibilidade](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para seu aplicativo. Essa configuração envolve a criação de vários tooensure VMs que pelo menos um está em execução.

Para sua tooqualify de implantação para o contrato de nível de serviço 99.95 VM, é necessário toodeploy duas ou mais VMs em execução dentro de sua carga de trabalho uma [conjunto de disponibilidade](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Essa configuração garante que as VMs sejam distribuídas entre vários domínios de falha e implantadas em hosts com janelas de manutenção diferentes. Olá completo [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explica Olá garantida de disponibilidade do Azure como um todo.

### <a name="back-up-hello-vm"></a>Fazer backup Olá VM
Um [Cofre de serviços de recuperação](../../backup/backup-introduction-to-azure-backup.md) é usado tooprotect dados e ativos nos serviços de Backup do Azure e o Azure Site Recovery. Você pode usar um cofre de serviços de recuperação muito[implantar e gerenciar backups para VMs implantadas pelo Gerenciador de recursos usando o PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Próximas etapas
* Se sua intenção for toowork com VMs do Linux, examine [Azure e do Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Saiba mais sobre as diretrizes de saudação em torno de configuração de sua infraestrutura de saudação [passo a passo de infraestrutura do Azure de exemplo](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
