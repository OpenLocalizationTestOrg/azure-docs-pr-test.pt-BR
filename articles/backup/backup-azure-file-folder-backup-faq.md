---
title: Perguntas frequentes do agente de Backup do Azure | Microsoft Docs
description: "Respostas a perguntas comuns sobre: como funciona o agente de backup do Azure, o backup e os limites de retenção."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "backup e recuperação de desastre; serviço de backup"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: 227cdc87f3e2c8ed393145f4bbde7f74606bdf3b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="questions-about-the-azure-backup-agent"></a>Perguntas sobre o agente de Backup do Azure
Este artigo possui respostas para perguntas comuns para ajudar você a compreender rapidamente os componentes do agente de Backup do Azure. Em algumas das respostas, há links para artigos com informações abrangentes. Você também pode postar perguntas sobre o serviço de Backup do Azure no [fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurar o backup
### <a name="where-can-i-download-the-latest-azure-backup-agent-br"></a>Onde posso baixar o agente mais recente do Backup do Azure? <br/>
Você pode baixar o agente mais recente para fazer backup do Windows Server, do System Center DPM ou do cliente Windows [daqui](http://aka.ms/azurebackup_agent). Se você quiser fazer backup de uma máquina virtual, use o Agente de VM (que instala automaticamente a extensão apropriada). O Agente de VM já está presente em máquinas virtuais criadas na galeria do Azure.

### <a name="when-configuring-the-azure-backup-agent-i-am-prompted-to-enter-the-vault-credentials-do-vault-credentials-expire"></a>Ao configurar o agente do Backup do Azure, preciso inserir as credenciais do cofre. As credenciais do cofre expiram?
Sim, as credenciais do cofre expiram após 48 horas. Se o arquivo expirar, faça logon no Portal do Azure e baixe os arquivos de credenciais de cofre no seu cofre.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Em que tipos de unidades posso fazer backup de arquivos e pastas? <br/>
Você não pode fazer backup das unidades/volumes a seguir:

* Mídia removível: todas as fontes de item de backup devem ser indicadas como fixas.
* Volumes somente leitura: o volume deve ser gravável para que o VSS (Serviço de Cópias de Sombra de Volume) funcione.
* Volumes offline: o volume deve estar online para que o VSS funcione.
* Compartilhamento de rede: O volume deve ser local para o backup do servidor usando o backup online.
* Volumes protegidos pelo Bitlocker: o volume deve ser desbloqueado antes de ser possível realizar o backup.
* Identificação do sistema de arquivos: NTFS é o único sistema de arquivos com suporte.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>De quais tipos de arquivo e pasta no servidor posso fazer backup?<br/>
Os seguintes tipos têm suporte:

* Criptografado
* Compactado
* Esparsos
* Compactado + esparso
* Links físicos: sem suporte, ignorado
* Ponto de nova análise: sem suporte, ignorado
* Criptografado + esparso: sem suporte, ignorado
* Fluxo compactado: sem suporte, ignorado
* Fluxo esparso: sem suporte, ignorado

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-already-backed-by-the-azure-backup-service-using-the-vm-extension-br"></a>Posso instalar o agente de Backup do Azure em uma VM do Azure da qual o serviço de Backup do Azure já fez backup usando a extensão de VM? <br/>
Com certeza. O Backup do Azure fornece backup no nível de VM para as máquinas virtuais do Azure usando a extensão de VM. Para proteger arquivos e pastas no SO Windows convidado, instale o agente de Backup do Azure no SO Windows convidado .

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-to-back-up-files-and-folders-present-on-temporary-storage-provided-by-the-azure-vm-br"></a>Posso instalar o agente de Backup do Azure em uma VM do Azure para fazer backup de arquivos e pastas presentes no armazenamento temporário fornecido pela VM do Azure? <br/>
Sim. Instale o agente de Backup do Azure no SO convidado do Windows e faça backup de arquivos e de pastas em um armazenamento temporário. Os trabalhos de backup falham assim que os dados do armazenamento temporário são apagados. Além disso, se os dados de armazenamento temporário tiverem sido excluídos, você só poderá restaurar em um armazenamento não volátil.

### <a name="whats-the-minimum-size-requirement-for-the-cache-folder-br"></a>Qual é o requisito de tamanho mínimo para a pasta de cache? <br/>
O tamanho da pasta de cache determina a quantidade de dados submetida a backup. Sua pasta de cache deve ter 5% do espaço necessário para o armazenamento de dados.

### <a name="how-do-i-register-my-server-to-another-datacenterbr"></a>Como registro meu servidor em outro datacenter?<br/>
Os dados de backup são enviados ao datacenter do cofre para o qual ele está registrado. A maneira mais fácil de alterar o datacenter é desinstalar o agente e reinstalá-lo e registrar um novo cofre que pertença ao datacenter desejado.

### <a name="does-the-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>O agente de Backup do Azure funciona em um servidor que usa a eliminação de duplicação do Windows Server 2012? <br/>
Sim. O serviço do agente converte os dados com eliminação de duplicação para dados normais quando prepara a operação de backup. Ele então otimiza os dados para backup, criptografa os dados e envia os dados criptografados para o serviço de backup online.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-the-cache-location-specified-for-the-azure-backup-agentbr"></a>Como posso alterar o local de cache especificado para o agente de Backup do Azure?<br/>
Use a lista a seguir para alterar o local do cache.

1. Pare o mecanismo do Backup ao executar o seguinte comando em um prompt de comando com privilégios elevados:

    ```PS C:\> Net stop obengine``` 
  
2. Não mova os arquivos. Em vez disso, copie a pasta de espaço de cache para outra unidade com espaço suficiente. O espaço em cache original pode ser removido após a confirmação de que os backups estão funcionando com o novo espaço em cache.
3. Atualize as entradas do registro a seguir com o caminho para a nova pasta de espaço em cache.<br/>

    | Caminho do registro | Chave do Registro | Valor |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Novo local da pasta de cache* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Novo local da pasta de cache* |

4. Reinicie o mecanismo do Backup ao executar o seguinte comando em um prompt de comando com privilégios elevados:

    ```PS C:\> Net start obengine```

Assim que a criação do backup for concluída com êxito no novo local de cache, você poderá remover a pasta de cache original.


### <a name="where-can-i-put-the-cache-folder-for-the-azure-backup-agent-to-work-as-expectedbr"></a>Onde posso colocar a pasta de cache para o Agente de Backup do Azure para que ele funcione conforme o esperado?<br/>
Os locais a seguir para a pasta de cache não são recomendados:

* Compartilhamento de rede ou Mídia Removível: a pasta de cache deve ser local para o servidor que precisa de backup usando o backup online. Não há suporte para os locais de rede ou para a mídia removível como unidades USB.
* Volumes Offline: a pasta de cache deve estar online para o backup esperado com o Agente de Backup do Azure.

### <a name="are-there-any-attributes-of-the-cache-folder-that-are-not-supportedbr"></a>Existe algum atributo da pasta de cache que não tenha suporte?<br/>
Os atributos a seguir, ou suas combinações, não têm suporte para a pasta de cache:

* Criptografado
* Eliminação de duplicação
* Compactado
* Esparsos
* Ponto de nova análise

A pasta de cache e o VHD dos metadados não têm os atributos necessários para o agente de Backup do Azure.

### <a name="is-there-a-way-to-adjust-the-amount-of-bandwidth-used-by-the-backup-servicebr"></a>Há uma maneira de ajustar a quantidade de largura de banda usada pelo serviço de Backup?<br/>
  Sim, use a opção **Alterar Propriedades** no Agente de Backup para ajustar a largura de banda. Você pode ajustar a quantidade de largura de banda e os horários quando usar essa largura de banda. Para obter instruções passo a passo, consulte  **[Habilitar limitação de rede](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Gerenciar backups
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-to-azurebr"></a>O que acontece se eu renomear um servidor Windows que está fazendo backup de dados no Azure?<br/>
Ao renomear um servidor, todos os backups configurados atualmente serão interrompidos.
Registre o novo nome do servidor no Cofre de Backup. Ao registrar o novo nome com o cofre, a primeira operação de backup é um backup *completo*. Se você precisar recuperar dados de backup para o cofre com o nome antigo do servidor, use a opção [**Outro servidor**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) no assistente **Recuperar dados**.

### <a name="what-is-the-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Qual é o comprimento máximo do caminho do arquivo que pode ser especificado no Backup do Azure usando o agente de Backup do Azure? <br/>
O agente de Backup do Azure baseia-se em NTFS. A [especificação de comprimento de caminho de arquivo é limitada pela API do Windows](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Se os arquivos que você deseja proteger tiverem um comprimento de caminho de arquivo maior do que o que é permitido pela API do Windows, faça backup da pasta pai ou da unidade de disco.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Quais caracteres são permitidos no caminho de arquivo da política de Backup do Azure usando o agente de Backup do Azure? <br>
 O agente de Backup do Azure baseia-se em NTFS. Ele permite os [caracteres com suporte do NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) como parte da especificação de arquivo. 
 
### <a name="i-receive-the-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Recebo o aviso "Os Backups do Azure não foram configurados para este servidor" embora tenha agendado configurado uma política de backup <br/>
Esse aviso ocorre quando as configurações de agendamento de backup armazenadas no servidor local não são iguais às configurações armazenadas no cofre de backup. Quando o servidor ou as configurações tiverem sido recuperadas para um bom estado conhecido, os agendamentos de backup podem perder a sincronização. Se você receber esse aviso, [reconfigure a política de backup](backup-azure-manage-windows-server.md) e escolha **Executar o Backup Agora** para sincronizar novamente o servidor local com o Azure.
