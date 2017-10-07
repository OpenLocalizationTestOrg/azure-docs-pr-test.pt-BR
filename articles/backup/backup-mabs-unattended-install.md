---
title: "instalação de aaaSilent do servidor de Backup do Azure v2 | Microsoft Docs"
description: "Use um toosilently de script do PowerShell instalar servidor de Backup do Azure v2. Esse tipo de instalação também é chamado de uma instalação autônoma."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Executar uma instalação autônoma do Servidor de Backup do Azure v2

Saiba como toorun uma instalação autônoma do servidor de Backup do Azure v2. 

Essas etapas não se aplicam se você estiver instalando o Servidor de Backup do Azure v1.

## <a name="install-backup-server-v2"></a>Instalar o Servidor de Backup v2

1. No servidor de saudação que hospeda o servidor de Backup do Azure v2, crie um arquivo de texto. (Você pode criar arquivo hello no bloco de notas ou em outro texto editor.) Salve o arquivo hello como MABSSetup.ini. 

2. Colar Olá código Olá MABSSetup.ini arquivo a seguir. Substituir o texto de saudação dentro de colchetes hello (\< \>) com valores do seu ambiente. Olá texto a seguir é um exemplo:

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Salve o arquivo hello. Em seguida, em um prompt de comando elevado no servidor de instalação hello, digite este comando:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Você pode usar esses sinalizadores para a instalação de saudação:</br>
**/f**: .ini caminho do arquivo</br>
**/l**: caminho do log</br>
**/i**: caminho de instalação</br>
**/x**: desinstalar o caminho</br>

## <a name="next-steps"></a>Próximas etapas
Depois de instalar o servidor de Backup, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.

- [Preparar as cargas de trabalho do Servidor de Backup](backup-azure-microsoft-azure-backup.md)
- [Usar o servidor de Backup tooback um servidor VMware](backup-azure-backup-server-vmware.md)
- [Usar o servidor de Backup tooback o SQL Server](backup-azure-sql-mabs.md)
- [Adicione o armazenamento de Backup modernos tooBackup Server](backup-mabs-add-storage.md)
