# Visão geral
## [Sobre máquinas virtuais](../../virtual-machines-windows-about.md)
## [Discos e VHDs](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
## [Redes Virtuais](../../../virtual-network/virtual-networks-overview.md)
## [Perguntas frequentes](faq.md)
## [Comparar VMs, sites e serviços de nuvem](../../../app-service-web/choose-web-site-cloud-service-vm.md)
## [Contêineres](../../virtual-machines-windows-containers.md)

# Introdução
## [Criar uma máquina virtual usando o portal de saudação](tutorial.md)
## [Faça logon no tooa VM](connect-logon.md)
## [Instale o Azure PowerShell](/powershell/azure/overview)
## [Instalar a CLI do Azure.](../../../cli-install-nodejs.md)

# Como

## Usar o Armazenamento
### [Anexar um disco de dados](attach-disk.md)
### [Desanexar um disco de dados](detach-disk.md)
### [Usar D: como um disco de dados](../../virtual-machines-windows-change-drive-letter.md)

## Rede
### [Como tooset pontos de extremidade](setup-endpoints.md)
### [Conectar VMs com uma VNet ou Serviço de Nuvem](connect-vms.md)
### [Conecte-se clássico VNets tooResource Manager VNets](../../../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
### [Criar um balanceador de carga](../../../load-balancer/load-balancer-get-started-internet-classic-portal.md)
### [Gerenciar NSGs usando o Azure PowerShell](../../../virtual-network/virtual-networks-create-nsg-classic-ps.md)

## Implantar
### [Criar uma VM personalizada](createportal.md)
### [Criar e configurar uma VM usando o Azure PowerShell](create-powershell.md)
### [Capturar uma VM do Windows](capture-image.md)
### [Criar e carregar um VHD usando o PowerShell](createupload-vhd.md)
### [Automatizar a implantação da VM do Azure com o Chef](../../virtual-machines-windows-chef-automation.md)
### [Criar e gerenciar VMs no Visual Studio](manage-visual-studio.md)
### [Criar uma VM para um aplicativo Web com o Visual Studio](web-app-visual-studio.md)
### [Executar uma tarefa com uso intensivo de computação no Java](java-run-compute-intensive-task.md)
### [Aplicativo Web Django Hello World](python-django-web-app.md)

## Configurar
### [Redefinir um serviço de área de trabalho remota de senha ou hello](../../virtual-machines-windows-reset-rdp.md)
### [Instalar e configurar o Symantec Endpoint Protection](install-symantec.md)
### [Instalar e configurar o Trend Micro Deep Security como Serviço](install-trend.md)
### [Configurar um conjunto de disponibilidade](configure-availability.md)
### [Redimensionar uma VM do Windows criada no modelo de implantação clássico Olá](resize-vm.md)
### [Manutenção](planned-maintenance-schedule.md)

## Gerenciar
### [Migração de clássico tooResource Manager](../../virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
### [Gerenciar suas VMs usando o Azure PowerShell](manage-psh.md)
### [Sobre extensões e agente de VM Olá](agents-and-extensions.md)
### [Gerenciar extensões de VM](manage-extensions.md)
### [Extensão de Script personalizado para VMs](extensions-customscript.md)
### [Injeção de dados personalizados em uma VM do Azure](inject-custom-data.md)

## Plano
### [Sobre imagens](about-images.md)
### [Tamanhos para VMs](../../virtual-machines-windows-sizes.md)
### [Manutenção planejada para VMs do Azure](../../virtual-machines-windows-planned-maintenance.md)
### [Diretrizes de implementação dos Serviços de Infraestrutura do Azure](../../virtual-machines-windows-infrastructure-subscription-accounts-guidelines.md)

## Gerenciar cargas de trabalho
### [HPC (Computação de Alto Desempenho)](../../virtual-machines-windows-hpcpack-cluster-options.md)
#### [Dimensionar os recursos automaticamente](hpcpack-cluster-node-autogrowshrink.md)
#### [Gerenciar nós de computação](hpcpack-cluster-node-manage.md)
#### [Criar um cluster](hpcpack-cluster-powershell-script.md)
#### [Configurar aplicativos de MPI de toorun um cluster](hpcpack-rdma-cluster.md)
#### [Executar cargas de trabalho do Excel e SOA](../../virtual-machines-windows-excel-cluster-hpcpack.md)
#### [Criar o nó principal Olá com uma imagem do Marketplace](../../virtual-machines-windows-hpcpack-cluster-headnode.md)
#### [Enviar trabalhos de tooAzure local](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md)
### [MongoDB](install-mongodb.md)
### [MySQL](mysql-2008r2.md)
### [Oracle](../../workloads/oracle/oracle-considerations.md)
### [SAP](sap-get-started.md)
### [SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
### [Tomcat](java-run-tomcat-app-server.md)

## Solucionar problemas
### [Conexões de Área de Trabalho Remota](../../virtual-machines-windows-troubleshoot-rdp-connection.md)
####[Etapas detalhadas de solução de problemas para problemas de conexão de área de trabalho remota](../../virtual-machines-windows-detailed-troubleshoot-rdp.md)
### [Aplicativo de tooan de acesso](../../virtual-machines-windows-troubleshoot-app-connection.md)
### [Problemas de implantação clássica ao criar uma nova VM](troubleshoot-deployment-new-vm.md)
### [Problemas de implantação clássica ao reiniciar ou redimensionar uma VM existente](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
### [Redefinir a senha RDP](reset-rdp.md)
### [Anexar o disco rígido virtual tootroubleshooting VM](troubleshoot-recovery-disks-portal.md)

# Referência
## [PowerShell](/powershell/azure/overview)
## [CLI do Azure](/cli/azure/vm)
## [Java](/java/api)
## [.NET](/dotnet/api/microsoft.azure.management.compute)
## [Criar modelos do Resource Manager](../../../resource-group-authoring-templates.md)
## [Modelos da comunidade](https://azure.microsoft.com/documentation/templates)
## [REST de computação](/rest/api/compute)
## [REST de rede](/rest/api)
## [REST de armazenamento](/rest/api/storageservices)

# Recursos
## [Roteiro do Azure](https://azure.microsoft.com/roadmap/?category=compute)
## [Preços](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)
## [Calculadora de preço](https://azure.microsoft.com/pricing/calculator/)
## [Disponibilidade regional](https://azure.microsoft.com/regions/services/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-machine)
## [Vídeos](https://azure.microsoft.com/documentation/videos/index/?services=virtual-machines)
