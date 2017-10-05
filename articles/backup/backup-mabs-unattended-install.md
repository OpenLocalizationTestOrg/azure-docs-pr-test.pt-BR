---
title: "Instalação silenciosa do Servidor de Backup do Azure v2 | Microsoft Docs"
description: "Use um script do PowerShell para instalar silenciosamente o Servidor de Backup do Azure v2. Esse tipo de instalação também é chamado de uma instalação autônoma."
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="12825-104">Executar uma instalação autônoma do Servidor de Backup do Azure v2</span><span class="sxs-lookup"><span data-stu-id="12825-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="12825-105">Saiba como executar uma instalação autônoma do Servidor de Backup do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="12825-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="12825-106">Essas etapas não se aplicam se você estiver instalando o Servidor de Backup do Azure v1.</span><span class="sxs-lookup"><span data-stu-id="12825-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="12825-107">Instalar o Servidor de Backup v2</span><span class="sxs-lookup"><span data-stu-id="12825-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="12825-108">No servidor que hospeda o Servidor de Backup do Azure v2, crie um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="12825-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="12825-109">(Você pode criar o arquivo no Bloco de Notas ou em outro editor de texto.) Salve o arquivo como MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="12825-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="12825-110">Cole o código a seguir no arquivo MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="12825-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="12825-111">Substitua o texto dentro dos colchetes (\< \>) com valores do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="12825-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="12825-112">O texto a seguir é um exemplo:</span><span class="sxs-lookup"><span data-stu-id="12825-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="12825-113">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="12825-113">Save the file.</span></span> <span data-ttu-id="12825-114">Em seguida, em um prompt de comando com privilégios elevados no servidor de instalação, digite este comando:</span><span class="sxs-lookup"><span data-stu-id="12825-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="12825-115">Você pode usar esses sinalizadores para a instalação:</span><span class="sxs-lookup"><span data-stu-id="12825-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="12825-116">
**/f**: .ini caminho do arquivo</span><span class="sxs-lookup"><span data-stu-id="12825-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="12825-117">
**/l**: caminho do log</span><span class="sxs-lookup"><span data-stu-id="12825-117">
**/l**: Log path</span></span></br><span data-ttu-id="12825-118">
**/i**: caminho de instalação</span><span class="sxs-lookup"><span data-stu-id="12825-118">
**/i**: Installation path</span></span></br><span data-ttu-id="12825-119">
**/x**: desinstalar o caminho</span><span class="sxs-lookup"><span data-stu-id="12825-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="12825-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12825-120">Next steps</span></span>
<span data-ttu-id="12825-121">Depois de instalar o Servidor de Backup, saiba como preparar seu servidor, ou começar a proteger uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="12825-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="12825-122">Preparar as cargas de trabalho do Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="12825-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="12825-123">Usar o Servidor de Backup para fazer backup de um Servidor do VMware</span><span class="sxs-lookup"><span data-stu-id="12825-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="12825-124">Usar o Servidor de Backup para fazer backup de SQL Server</span><span class="sxs-lookup"><span data-stu-id="12825-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="12825-125">Adicionar Armazenamento de Backup Moderno para o Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="12825-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
