---
title: aaaOverview de VMs do Linux no Azure | Microsoft Docs
description: "Descreve os serviços de Computação, Armazenamento e Rede do Azure com máquinas virtuais Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure e Linux
O Microsoft Azure é uma coleção crescente de serviços de nuvem pública integrados, incluindo análise, Máquinas Virtuais, bancos de dados, mobilidade, rede, armazenamento, e Web&mdash;ideal para hospedar suas soluções.  O Microsoft Azure fornece uma plataforma de computação escalonável que permite que você tooonly pagamento para que você usa, quando desejar - sem ter que tooinvest no hardware local.  Azure está pronto quando estiver tooscale suas soluções de backup e fora de escala toowhatever precisar tooservice necessidades de saudação de seus clientes.

Se você estiver familiarizado com hello vários recursos da Amazon AWS, você pode examinar hello Azure vs AWS [documento de definição de mapeamento](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Regiões
Recursos do Microsoft Azure são distribuídos entre várias regiões geográficas em todo o mundo de saudação.  Uma "região" representa vários datacenters em uma única área geográfica.  Temos 34 regiões geralmente disponíveis em torno de Olá mundo com um regiões 4 adicionais anunciada. Como continuaremos tooexpand nossa cobertura global - mantemos que uma lista atualizada de existentes e recentemente anunciado regiões.

* [Regiões do Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Disponibilidade
Anunciamos que uma máquina de virtual de única instância líderes do setor contrato de nível de serviço de 99,9% fornecido a que você implantar Olá VM com o armazenamento premium para todos os discos.  Para que seu tooqualify de implantação para nosso padrão 99,95% contrato de nível de serviço de VM, você ainda precisará toodeploy duas ou mais VMs em execução dentro de um conjunto de disponibilidade de sua carga de trabalho. Isso garantirá que suas VMs sejam distribuídas entre vários domínios de falha em nossos datacenters, além de serem implantadas em hosts com janelas de manutenção diferentes. Olá completo [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explica Olá garantida de disponibilidade do Azure como um todo.

## <a name="managed-disks"></a>Managed Disks

Identificadores de armazenamento do Azure, criação de conta e gerenciamento no plano de fundo Olá para você e garante que você não tem tooworry sobre limites de escalabilidade Olá Olá da conta de armazenamento de discos de gerenciado. Você simplesmente especifica o tamanho de disco hello e camada de desempenho de saudação (Standard ou Premium), e o Azure cria e gerencia disco Olá para você. Mesmo que você adicione discos ou dimensionar Olá VM para cima e para baixo, você não tem tooworry sobre armazenamento hello está sendo usado. Se você estiver criando novas VMs, [usar hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou Olá VMs toocreate portal do Azure com discos de dados e sistema operacional gerenciado. Se você tiver VMs com discos não gerenciados, você pode [converter seu toobe VMs feito com discos gerenciados](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Você também pode gerenciar suas imagens personalizadas em uma conta de armazenamento por região do Azure e usá-los toocreate centenas de VMs em Olá mesma assinatura. Para obter mais informações sobre discos gerenciados, consulte Olá [visão geral de discos gerenciados](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Máquinas Virtuais e instâncias do Azure
O Microsoft Azure dá suporte à execução de várias distribuições populares do Linux fornecidas e mantidas por diversos parceiros.  Você encontrará distribuições como Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD e muito mais no hello Azure Marketplace. Ativamente trabalhamos com tooadd de comunidades Linux vários tipos ainda mais toohello [Azure aprovados Linux Distros](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lista.

Se a distribuição de Linux preferencial de escolha não está presente atualmente na Galeria de saudação, você pode "traga seu próprio Linux" VM por [criando e carregando um VHD do Linux no Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Máquinas virtuais do Azure permitem que você toodeploy uma ampla gama de soluções de computação de uma maneira ágil. Você pode implantar praticamente qualquer carga de trabalho e qualquer linguagem em praticamente qualquer sistema operacional, Windows, Linux, ou um personalizado criado de nossa lista cada vez maior de parceiros. Ainda não consegue encontrar o que você está procurando?  Não se preocupe: você também pode usar suas próprias imagens locais.

## <a name="vm-sizes"></a>Tamanhos de VM
Quando você implanta uma VM no Azure, você vai tooselect um tamanho de VM dentro de nossa série de tamanhos de carga de trabalho tooyour adequado. tamanho de saudação também afeta Olá poder de processamento, memória e capacidade de armazenamento de máquina virtual de saudação. Você será cobrado com base na quantidade de saudação do hello tempo VM está em execução e consumir seus recursos alocados. Uma lista completa de [tamanhos de Máquinas Virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aqui estão algumas diretrizes básicas para selecionar um tamanho de VM de uma de nossas séries (A, D, DS, G e GS).
* VMs da série A são nossas VMs básicas econômicas para cargas de trabalho leves e cenários de desenvolvimento e teste. Eles estão disponíveis em todas as regiões e podem se conectar e usar todas as máquinas de toovirtual disponíveis de recursos padrão.
* Os tamanhos da série A (A8 - A11) são configurações especiais com uso intensivo de computação adequadas para aplicativos de cluster com computação de alto desempenho.
* VMs série D são projetadas toorun aplicativos que exigem maior capacidade de computação e desempenho de disco temporário. VMs série D fornecem processadores mais rápidos, uma maior taxa de memória por núcleo e uma unidade de estado sólida (SSD) para o disco temporário hello.
* Série Dv2, é a versão mais recente Olá da nossa série D, apresenta uma CPU mais eficiente. Olá Dv2 série CPU é cerca de 35% mais rápido do que Olá CPU da série D. Ele se baseia Olá última geração v3 de 2,4 GHz Intel Xeon® E5-2673 processador (Haskell) e com hello Intel Turbo aumento tecnologia 2.0, pode subir too3.2 GHz. Olá Dv2 série tem Olá mesmas configurações de disco e memória conforme Olá série D.
* As VMs da série G oferecem hello mais memória e executadas em hosts que têm processadores da família Intel Xeon E5 V3.

Observação: Série DS e as VMs da série GS têm acesso tooPremium armazenamento - nosso SSD feito o armazenamento de alto desempenho e baixa latência para cargas de trabalho intensivas de e/s. O Armazenamento Premium está disponível em determinadas regiões. Para obter mais informações, consulte:

* [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho da máquina virtual do Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automação
uma cultura DevOps adequada, toda a infra-estrutura de tooachieve deve ser o código.  Quando todos os Olá infraestrutura vidas no código pode ser facilmente recriado (Phoenix servidores).  Azure funciona com todos os automação principais Olá ferramentas como Ansible, Chef, SaltStack e Puppet.  O Azure também tem suas próprias ferramentas de automação:

* [Modelos do Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [VMAccess do Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

O Azure está implementando o suporte para [cloud-init](http://cloud-init.io/) na maioria das Distribuições Linux que oferecem suporte a ele.  Atualmente, as VMs do Ubuntu Canonical são implantadas com cloud-init habilitado por padrão.  Fedora suporte init de nuvem, porém hello Azure, CentOS e Red chapéus RHEL imagens mantidas pelo RedHat não têm instalada de inicialização de nuvem.  toouse nuvem-init em uma sistema operacional da família de RedHat, crie uma imagem personalizada com a nuvem-init instalado.

* [Como usar o cloud-init em VMs Linux do Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Cotas
Cada assinatura do Azure tem limites de cota padrão que podem afetar a implantação de saudação de um grande número de máquinas virtuais para o seu projeto. o limite atual de saudação em uma base por assinatura é 20 VMs por região.  Os limites de cota podem ser aumentados de forma rápida e fácil com a emissão de um tíquete de suporte para solicitar um aumento de limite.  Para obter mais detalhes sobre os limites de cota:

* [Limites de Serviço da assinatura do Azure](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Parceiros
Microsoft trabalha em conjunto com nossos parceiros de imagens de saudação tooensure disponíveis são atualizadas e otimizadas para um tempo de execução do Azure.  Para saber mais sobre nossos parceiros, verifique a seguir suas páginas no Marketplace.

* Linux no Azure – [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE – [Azure Marketplace – SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat - [Azure Marketplace - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [Azure Marketplace - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Marketplace - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Azure Marketplace - CoreOS (Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami Library para Azure](https://azure.bitnami.com/)
* Mesosphere - [Azure Marketplace - Mesosphere DC/OS no Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Marketplace – Serviço de Contêiner do Azure com Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Introdução ao Linux no Azure
toobegin usando o Azure, você precisa de uma conta do Azure, Olá CLI do Azure instalado e um par de chaves públicas e privadas de SSH.

### <a name="sign-up-for-an-account"></a>Inscrever-se em uma conta
a primeira etapa Hello usando Olá nuvem do Azure é toosign para uma conta do Azure.  Vá toohello [inscrição de contas do Azure](https://azure.microsoft.com/pricing/free-trial/) página tooget iniciado.

### <a name="install-hello-cli"></a>Instalar Olá CLI
Com sua nova conta do Azure, você pode começar imediatamente usando Olá portal do Azure, que é um painel de administração baseado na web.  Olá toomanage nuvem do Azure por meio de saudação de linha de comando, você instala Olá `azure-cli`.  Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-azure-cli) na estação de trabalho Mac ou Linux.

### <a name="create-an-ssh-key-pair"></a>Criar um par de chaves SSH
Agora você tem uma conta do Azure, portal da web do Azure de saudação e Olá CLI do Azure.  Olá próxima etapa é toocreate um par de chaves de SSH é tooSSH usado em Linux sem usar uma senha.  [Criar chaves SSH no Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable sem senha logons e melhor segurança.

### <a name="create-a-vm-using-hello-cli"></a>Criar uma VM usando Olá CLI
Criando uma VM do Linux usar Olá CLI é toodeploy uma maneira rápida uma VM sem Olá terminal deixando que você está trabalhando.  Tudo o que você pode especificar no portal da web de saudação está disponível por meio de um sinalizador de linha de comando ou um comutador.  

* [Criar uma VM do Linux usando Olá CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Criar uma máquina virtual no portal de saudação
Criar uma VM do Linux no portal da web do Azure de saudação é uma maneira tooeasily ponto e clique em Olá vários implantação de tooa tooget de opções.  Em vez de usar sinalizadores de linha de comando ou opções, você é capaz de tooview um layout de web adequado de várias opções e configurações.  Todos os itens disponíveis por meio da interface de linha de comando Olá também estão disponível no portal de saudação.

* [Criar uma VM do Linux usando o Portal de saudação](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Fazer logon usando SSH sem uma senha
Olá VM está em execução no Azure e você está pronto toolog no.  Usar toolog senhas em via SSH é demorada e inseguras.  Usando as chaves de SSH é Olá a maneira mais segura e também Olá toologin de maneira mais rápida.  Quando você criar VM do Linux via portal hello ou hello CLI, você tem duas opções de autenticação.  Se você escolher uma senha para o SSH, o Azure configura logons de tooallow Olá VM por meio de senhas.  Se você escolheu toouse uma chave pública SSH, o Azure configura Olá VM tooonly permitir logons SSH chaves e desabilita os logons de senha. toosecure sua VM do Linux por apenas permitir logons de chave SSH, use Olá a opção de chave pública SSH durante a saudação criação de VM no portal de saudação ou CLI.

## <a name="related-azure-components"></a>Componentes relacionados do Azure
## <a name="storage"></a>Armazenamento
* [Introdução tooMicrosoft armazenamento do Azure](../../storage/common/storage-introduction.md)
* [Adicionar um tooa VM do Linux usando a cli do azure de saudação do disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Como tooattach dados de um disco tooa VM do Linux no hello portal do Azure](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Rede
* [Visão geral da Rede Virtual](../../virtual-network/virtual-networks-overview.md)
* [Endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Abrindo portas tooa VM do Linux no Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar um nome de domínio totalmente qualificado no hello portal do Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Contêineres
* [Máquinas virtuais e contêineres no Azure](containers.md)
* [Introdução ao Serviço de Contêiner do Azure](../../container-service/container-service-intro.md)
* [Implantar um cluster do Serviço de Contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Próximas etapas
Agora você tem uma visão geral do Linux no Azure.  Olá próxima etapa é toodive em e criar algumas VMs!

* [Explore nossa lista crescente de Scripts de Exemplo para tarefas comuns via AzureCLI](cli-samples.md)
