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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="3c2db-104">Executar uma instalação autônoma do Servidor de Backup do Azure v2</span><span class="sxs-lookup"><span data-stu-id="3c2db-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="3c2db-105">Saiba como toorun uma instalação autônoma do servidor de Backup do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="3c2db-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="3c2db-106">Essas etapas não se aplicam se você estiver instalando o Servidor de Backup do Azure v1.</span><span class="sxs-lookup"><span data-stu-id="3c2db-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="3c2db-107">Instalar o Servidor de Backup v2</span><span class="sxs-lookup"><span data-stu-id="3c2db-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="3c2db-108">No servidor de saudação que hospeda o servidor de Backup do Azure v2, crie um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="3c2db-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="3c2db-109">(Você pode criar arquivo hello no bloco de notas ou em outro texto editor.) Salve o arquivo hello como MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="3c2db-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="3c2db-110">Colar Olá código Olá MABSSetup.ini arquivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3c2db-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="3c2db-111">Substituir o texto de saudação dentro de colchetes hello (\< \>) com valores do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3c2db-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="3c2db-112">Olá texto a seguir é um exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c2db-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="3c2db-113">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="3c2db-113">Save hello file.</span></span> <span data-ttu-id="3c2db-114">Em seguida, em um prompt de comando elevado no servidor de instalação hello, digite este comando:</span><span class="sxs-lookup"><span data-stu-id="3c2db-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="3c2db-115">Você pode usar esses sinalizadores para a instalação de saudação:</span><span class="sxs-lookup"><span data-stu-id="3c2db-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="3c2db-116">
**/f**: .ini caminho do arquivo</span><span class="sxs-lookup"><span data-stu-id="3c2db-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="3c2db-117">
**/l**: caminho do log</span><span class="sxs-lookup"><span data-stu-id="3c2db-117">
**/l**: Log path</span></span></br><span data-ttu-id="3c2db-118">
**/i**: caminho de instalação</span><span class="sxs-lookup"><span data-stu-id="3c2db-118">
**/i**: Installation path</span></span></br><span data-ttu-id="3c2db-119">
**/x**: desinstalar o caminho</span><span class="sxs-lookup"><span data-stu-id="3c2db-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="3c2db-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c2db-120">Next steps</span></span>
<span data-ttu-id="3c2db-121">Depois de instalar o servidor de Backup, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3c2db-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="3c2db-122">Preparar as cargas de trabalho do Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="3c2db-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="3c2db-123">Usar o servidor de Backup tooback um servidor VMware</span><span class="sxs-lookup"><span data-stu-id="3c2db-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="3c2db-124">Usar o servidor de Backup tooback o SQL Server</span><span class="sxs-lookup"><span data-stu-id="3c2db-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="3c2db-125">Adicione o armazenamento de Backup modernos tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="3c2db-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
