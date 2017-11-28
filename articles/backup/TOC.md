
# Visão geral
## [O que é o Backup do Azure?](backup-introduction-to-azure-backup.md)

# Introdução
## [Fazer backup de VMs do Azure](backup-azure-vms-first-look-arm.md)
## [Fazer backup do Windows Server ou de computadores com Windows](backup-try-azure-backup-in-10-mins.md)
## [Fazer backup dos servidores VMware](backup-azure-backup-server-vmware.md)

# Como

## Servidor de Backup do Azure
### [Matriz de proteção do Servidor de Backup do Azure](backup-mabs-protection-matrix.md)
### Instalar ou atualizar
#### [Preparar cargas de trabalho do Servidor de Backup do Azure no portal do Azure](backup-azure-microsoft-azure-backup.md)
#### [Preparar cargas de trabalho do Servidor de Backup do Azure no portal clássico](backup-azure-microsoft-azure-backup-classic.md)
#### [Adicionar armazenamento tooAzure fazer Backup do servidor](backup-mabs-add-storage.md)
#### [Atualizar o servidor de Backup do Azure toov.2](backup-mabs-upgrade-to-v2.md)
#### [Instalação autônoma do Servidor de Backup do Azure](backup-mabs-unattended-install.md)
### Proteger as cargas de trabalho
#### [Usar o Azure Backup Server tooback um servidor VMware](backup-azure-backup-server-vmware.md)
#### [Usar o Azure Backup Server tooback o Exchange](backup-azure-exchange-mabs.md)
#### [Usar o Azure Backup Server tooback a um farm do SharePoint](backup-azure-backup-sharepoint-mabs.md)
#### [Usar o Azure Backup Server tooback SQL](backup-azure-sql-mabs.md)
#### [Proteger o estado do sistema e recuperação bare-metal](backup-mabs-system-state-and-bmr.md)
### [Recuperar dados de outro Servidor de Backup do Azure](backup-azure-alternate-dpm-server.md)

## VMs do Azure
### Preparar Olá VM
#### [Preparar as máquinas virtuais implantadas pelo Resource Manager](backup-azure-arm-vms-prepare.md)
#### [Backups consistentes do aplicativo das VMs Linux](backup-azure-linux-app-consistent.md)
#### [Preparar máquinas virtuais do Azure](backup-azure-vms-prepare.md)
### Planejar seu ambiente
#### [Planejar a infraestrutura de backup de VMs](backup-azure-vms-introduction.md)
### Fazer backup de VMs
#### [Fazer backup de máquinas virtuais do Azure cofre dos serviços de recuperação de tooa](backup-azure-arm-vms.md)
#### [Fazer backup de máquinas virtuais criptografadas](backup-azure-vms-encryption.md)
#### [Fazer backup de máquinas virtuais do Azure](backup-azure-vms.md)
### Gerenciar e monitorar VMs
#### [Gerenciar backups de VM do Azure no Portal do Azure](backup-azure-manage-vms.md)
#### [Monitorar alertas de backups de VM do Azure no Portal do Azure](backup-azure-monitor-vms.md)
#### [Gerenciar e monitorar os backups de VM do Azure no Portal Clássico](backup-azure-manage-vms-classic.md)
### Restaurar dados das VMs
#### [Recuperar arquivos de backups de VM do Azure](backup-azure-restore-files-from-vm.md)
#### [Restaurar VMs implantadas com o Resource Manager na Portal do Azure](backup-azure-arm-restore-vms.md)
#### [Restaurar máquinas virtuais criptografadas](backup-azure-vms-encryption.md)
#### [Restaurar máquinas virtuais no Azure](backup-azure-restore-vms.md)
#### [Restaurar chave e segredo do Key Vault para VMs criptografadas](backup-azure-restore-key-secret.md)

## Configurar relatórios de Backup do Azure
### [Configurar relatórios de Backup do Azure](backup-azure-configure-reports.md)
### [Modelo de dados para os relatórios de Backup do Azure](backup-azure-reports-data-model.md)
### [Modelo de dados do Log Analytics para o Backup do Azure](backup-azure-log-analytics-data-model.md)

## Data Protection Manager
### [Preparar as cargas de trabalho do DPM no portal do Azure](backup-azure-dpm-introduction.md)
### [Preparar as cargas de trabalho do DPM no portal clássico](backup-azure-dpm-introduction-classic.md)
### [Usar o System Center DPM tooback o Exchange server](backup-azure-backup-exchange-server.md)
### [Recuperar o servidor DPM alternativo de tooan dados](backup-azure-alternate-dpm-server.md)
### [Usar o DPM tooback cargas de trabalho do SQL Server](backup-azure-backup-sql.md)
### [Usar o DPM tooback a um farm do SharePoint](backup-azure-backup-sharepoint.md)

## Usar o PowerShell
### [VMs do Azure no portal do Azure](backup-azure-vms-automation.md)
### [VMs do Azure no portal clássico](backup-azure-vms-classic-automation.md)
### [DPM no portal do Azure](backup-dpm-automation.md)
### [DPM no portal clássico](backup-dpm-automation-classic.md)
### [Windows Server no portal do Azure](backup-client-automation.md)
### [Windows Server no portal clássico](backup-client-automation-classic.md)

## Banco de Dados SQL do Azure
### [Configurar retenção de backup de longo prazo](../sql-database/sql-database-configure-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Exibir backups em um cofre dos Serviços de Recuperação](../sql-database/sql-database-view-backups-in-vault.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Restaurar desde a retenção de backup de longo prazo](../sql-database/sql-database-restore-from-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Excluir backups de longo prazo do SQL do Azure](../sql-database/sql-database-long-term-retention-delete.md?toc=%2fazure%2fbackup%2ftoc.json)

## Windows Server
### [Fazer backup de pastas e arquivos do Windows Server](backup-configure-vault.md)
### [Fazer backup do Estado do Sistema do Windows Server](backup-azure-system-state.md)
### [Recuperar arquivos do servidor de tooWindows do Azure](backup-azure-restore-windows-server.md)
### [Restaurar o Estado do Sistema do Windows Server](backup-azure-restore-system-state.md)
### [Monitorar e gerenciar cofres dos Serviços de Recuperação](backup-azure-manage-windows-server.md)
### Fazer backup e restaurar usando o portal clássico Olá
#### [Windows Server usando o modelo de implantação clássico Olá](backup-configure-vault-classic.md)
#### [Gerenciar os cofres de Backup usando o modelo de implantação clássico Olá](backup-azure-manage-windows-server-classic.md)
#### [Recuperar arquivos tooa Windows Server usando o modelo de implantação clássico Olá](backup-azure-restore-windows-server-classic.md)

## Cofre dos Serviços de Recuperação
### [Visão geral de cofres de Serviços de Recuperação](backup-azure-recovery-services-vault-overview.md)
### [Atualizando um cofre de serviços de tooRecovery de Cofre de Backup](backup-azure-upgrade-backup-to-recovery-services.md)
### [Excluir um cofre dos Serviços de Recuperação](backup-azure-delete-vault.md)

## Solucionar problemas
### [Problemas de backup de VM do Azure no portal do Azure](backup-azure-vms-troubleshoot.md)
### [Problemas de backup de VM do Azure no portal clássico](backup-azure-vms-troubleshoot-classic.md)
### [Falha no Backup de VM do Azure: não foi possível se comunicar com o agente de VM Olá para status do snapshot - subtarefa de VM do instantâneo atingiu o tempo limite](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md)
### [Lentidão de backup de arquivos e pastas no Backup do Azure](backup-azure-troubleshoot-slow-backup-performance-issue.md)
### [Solucionar problemas de Servidor de Backup do Azure](backup-azure-mabs-troubleshoot.md)

# Conceitos

## Perguntas frequentes
### [Perguntas frequentes sobre o cofre de Serviços de Recuperação](backup-azure-backup-faq.md)
### [Perguntas frequentes sobre o backup de VM do Azure](backup-azure-vm-backup-faq.md)
### [Perguntas frequentes sobre o backup da pasta de arquivos usando o Agente de Backup do Azure](backup-azure-file-folder-backup-faq.md)

## [Controle de acesso baseado em função](backup-rbac-rs-vault.md)
## [Segurança para backups híbridos](backup-azure-security-feature.md)
## [Configurar o backup offline](backup-azure-backup-import-export.md)
## [Substitua sua biblioteca de fitas](backup-azure-backup-cloud-as-tape.md)


# Referência
## [PowerShell](/powershell/module/azurerm.recoveryservices.backup)
## [.NET](/dotnet/api/microsoft.azure.management.recoveryservices.backup)

# Recursos
## [Roteiro do Azure](https://azure.microsoft.com/roadmap/)
## [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowsazureonlinebackup)
## [Preços](https://azure.microsoft.com/pricing/details/backup/)
## [Calculadora de preço](https://azure.microsoft.com/pricing/calculator/)
## [Atualizações de serviço](https://azure.microsoft.com/updates/?product=backup)
## [Vídeos](https://azure.microsoft.com/documentation/videos/index/?services=backup)
