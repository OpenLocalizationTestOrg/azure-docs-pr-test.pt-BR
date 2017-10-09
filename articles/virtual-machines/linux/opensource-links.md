---
title: "aaaLinux e código-fonte aberto de computação no Azure | Microsoft Docs"
description: "Lista de artigos sobre Computação Linux e de software livre no Azure, incluindo o uso básico do Linux, alguns fundamentos sobre como executar ou carregar imagens do Linux no Azure e outro conteúdo sobre tecnologias e otimizações específicas."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Computação Linux e Software Livre no Azure
Localize a documentação de saudação todos os necessário toocreate e gerenciar máquinas virtuais baseadas em Linux modelo de implantação clássico hello.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="get-started"></a>Introdução
* [Introdução ao Linux no Azure](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Perguntas frequentes sobre máquinas virtuais do Azure criado com o modelo de implantação clássico Olá](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Sobre imagens de máquinas virtuais](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Carregar sua própria imagem de distribuição](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (e também instruções do uso de uma [Distribuição endossada pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))
* [Faça logon no tooa VM do Linux usando Olá portal clássico do Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Configurar
* [Instalar a CLI do Azure (interface de linha de comando do Azure)](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Tutoriais
* [Instalar Olá pilha LAMP em uma máquina virtual do Linux no Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Aplicativo Web Ruby on Rails Web em uma VM do Azure](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [Como instalar o Apache Qpid Proton-C para AMQP e barramento de serviço](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Bancos de dados
* [Otimizar o desempenho do MySQL no Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Clusters MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Executando Cassandra com Linux no Azure e acessando-a do Node.js](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Criar um cluster multimestre de MariaDbs](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar um aplicativo de MPI toorun Linux RDMA cluster](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Usando a extensão da VM Docker de saudação do hello Azure Interface de linha de comando (CLI do Azure)](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Usando Olá extensão da VM Docker do hello portal do Azure](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Como toouse docker-máquina no Azure](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [Como usar clusters MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Como usar Node.js e Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [Como instalar e executar o MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [Como usar o CoreOS no Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Planejamento
* [Diretrizes de implementação dos Serviços de Infraestrutura do Azure](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Selecionando nomes de usuário do Linux](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Como tooconfigure um conjunto de disponibilidade para máquinas virtuais no modelo de implantação clássico Olá](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Como tooSchedule manutenção planejada em VMs do Azure](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Gerenciar a disponibilidade de saudação de máquinas virtuais](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Manutenção planejada para máquinas virtuais Linux no Azure](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Implantação
* [Como criar uma máquina virtual personalizada que executa o Linux](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Olá Noções básicas: capturar um tooMake de VM do Linux um modelo](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informações para as distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>Gerenciamento
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Como tooReset uma senha ou SSH propriedades para Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Usando raiz](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Recursos do Azure.
* [Olá agente Linux do Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Recursos e extensões de VM do Azure](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Injeção de dados personalizado em uma VM toouse com init de nuvem](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Armazenamento
* [Anexando um disco de dados de tooa VM do Linux](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Desanexando um disco de dados de uma VM Linux](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Rede
* [Como tooset pontos de extremidade em uma máquina virtual clássica no Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Solucionar problemas
* [Solucionar problemas de Secure Shell (SSH) conexões tooa baseados em Linux máquina virtual do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Solucionar problemas de implantação clássica ao criar uma nova máquina virtual Linux no Azure](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma Máquina Virtual Linux existente no Azure](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>Referência
* [Comandos da CLI do Azure no modo ASM (Gerenciamento de Serviços do Azure)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [API REST de Gerenciamento de Serviços do Azure](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Links de geral
Olá links a seguir é para blogs da Microsoft, páginas do Technet e sites externos em vez de documentação Azure.com acima. Como o Azure e Olá mundo de computação de código-fonte aberto são ágeis destinos, é quase certeza de que Olá links a seguir estão desatualizadas, *apesar* fatos Olá que deverá fazemos nosso melhor toocontinually tópicos mais recentes de adicionar e remover aqueles desatualizadas. Se nós perdeu um,. avise-nos saber em comentários hello, ou enviar um tooour de solicitação pull [repositório GitHub](https://github.com/Azure/azure-content/).

* [Executando ASP.NET 5 em Linux usando contêineres de Docker](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [Como tooDeploy uma imagem de VM CentOS da OpenLogic](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [Infraestrutura de atualização SUSE](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server para SAP Cloud Appliance Library](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Criando Linux altamente disponível no Azure em 12 etapas](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Automatizar o provisionamento do Linux no Azure com a CLI do Azure, node.js, jhawk](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [GlusterFS no Azure](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [Executando FreeBSD no Azure](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [Implante FreeBSD facilmente](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [Implantando uma imagem de FreeBSD personalizada](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky AV para servidor de arquivos Linux](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [Oito bancos de dados NoSql de software livre para o Azure](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech): experiências com o CouchDb no Azure](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [Executando CouchDB como serviço com node.js, CORS e Grunt](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Redis no Windows em Olá serviço de Cache Redis do Azure](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [Anunciando o provedor de estado de sessão ASP.NET para a versão de teste do Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog: RavenHQ agora está disponível em hello Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Big Data
* [Instalando Hadoop em VMs Linux do Azure](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>Banco de dados relacional
* [Arquitetura de alta disponibilidade do MySQL no Microsoft Azure](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Instalando o Postgres com corosync, pg_bouncer usando ILB](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Computação de alto desempenho do Linux (HPC)
* [Modelo de início rápido: criar um cluster SLURM](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (e [postagem de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Modelo de início rápido: criar um cluster HPC com nós de computação Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>Desenvolvimentos, gerenciamento e otimização
Olá mundo de devops, gerenciamento e a otimização é muito extenso e alterar muito rapidamente, você deve considerar a lista de saudação abaixo de um ponto de partida.

* [Vídeo: Azure Virtual Machines: Using Chef, Puppet and Docker for managing Linux VMs (Máquinas virtuais do Azure: usando Chef, Puppet e Docker para gerenciar VMs Linux)](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [Concluir a implantação de cluster do guia tooautomated Kubernetes com CoreOS e Trança](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Visualizador do Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Plug-in de subordinado Jenkins para o Azure](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [Repositório GitHub: plug-in de armazenamento Jenkins do Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Terceiros: plug-in de subordinado Hudson do Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Terceiros: plug-in de armazenamento Hudson do Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Vídeo: o que é o Chef e como ele funciona?](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Vídeo: Como tooUse automação do Azure com VMs do Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog: Como toodo Powershell DSC para Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: Cliente Docker DSC](https://github.com/anweiss/DockerClientDSC)
* [Plug-in Packer para o Azure](https://github.com/msopentech/packer-azure)

