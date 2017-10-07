---
title: Agente de Backup aaaAzure perguntas Frequentes | Microsoft Docs
description: "Respostas a perguntas toocommon sobre: Olá como limites de funciona, backup e retenção de agente de backup do Azure."
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
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Perguntas sobre o agente de Backup do Azure Olá
Este artigo possui respostas toocommon perguntas toohelp componentes do agente de Backup do Azure Olá você compreender rapidamente. Em algumas das respostas hello, há artigos de toohello links com informações abrangentes. Você também pode postar perguntas sobre Olá serviço Backup do Azure no hello [Fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurar o backup
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Onde posso baixar o agente de Backup do Azure mais recente Olá? <br/>
Você pode baixar o agente mais recente hello para fazer backup do Windows Server, o System Center DPM ou o cliente do Windows, de [aqui](http://aka.ms/azurebackup_agent). Se você quiser tooback uma máquina virtual, use Olá agente de VM (que instala automaticamente o ramal apropriado Olá). Olá VM Agent já está presente nas máquinas virtuais criadas de saudação Galeria do Azure.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Ao configurar o agente de Backup do Azure Olá, eu sou tooenter solicitadas as credenciais do Cofre de saudação. As credenciais do cofre expiram?
Sim, as credenciais do cofre Olá expiram após 48 horas. Se o arquivo hello expirar, arquivos de log em toohello Azure portal e baixe Olá cofre credenciais do seu cofre.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Em que tipos de unidades posso fazer backup de arquivos e pastas? <br/>
Você não pode fazer backup Olá unidades/volumes a seguir:

* Mídia removível: todas as fontes de item de backup devem ser indicadas como fixas.
* Volumes somente leitura: volume Olá deve ser gravável para Olá volume shadow copy service (VSS) toofunction.
* Os Volumes offline: volume Olá deve estar online para toofunction do VSS.
* Compartilhamento de rede: volume Olá deve ser local toohello server toobe backup usando o backup online.
* Volumes protegidos pelo BitLocker: volume Olá deve ser desbloqueado antes Olá backup pode ser realizado.
* Identificação do sistema de arquivos: NTFS é Olá único sistema de arquivos com suporte.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>De quais tipos de arquivo e pasta no servidor posso fazer backup?<br/>
Olá tipos a seguir têm suporte:

* Criptografado
* Compactado
* Esparsos
* Compactado + esparso
* Links físicos: sem suporte, ignorado
* Ponto de nova análise: sem suporte, ignorado
* Criptografado + esparso: sem suporte, ignorado
* Fluxo compactado: sem suporte, ignorado
* Fluxo esparso: sem suporte, ignorado

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Pode instalar o agente de Backup do Azure Olá em uma VM do Azure já feito pelo serviço de Backup do Azure hello usando Olá extensão da VM? <br/>
Com certeza. Backup do Azure fornece backup em nível de VM para máquinas virtuais do Azure usando a extensão de VM hello. tooprotect arquivos e pastas no convidado Olá sistema operacional Windows, instale o agente de Backup do Azure de Olá no sistema operacional Windows de convidado de saudação.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Pode instalar o agente de Backup do Azure Olá em tooback uma VM do Azure backup de arquivos e pastas presentes no armazenamento temporário fornecido pelo Olá VM do Azure? <br/>
Sim. Instalar hello Azure Backup agent no sistema operacional Windows de convidado de saudação e fazer backup de arquivos e pastas de armazenamento de tootemporary. Os trabalhos de backup falham assim que os dados do armazenamento temporário são apagados. Além disso, se os dados de armazenamento temporário de saudação foi excluídos, você só pode restaurar armazenamento toonon volátil.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>O que é o requisito de tamanho mínimo de saudação para pasta de cache Olá? <br/>
tamanho de saudação da pasta de cache de saudação determina a quantidade de saudação de dados que você está fazendo backup. Sua pasta de cache deve ser de 5% de espaço de saudação necessário para armazenamento de dados.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Como registrar o datacenter de tooanother meu servidor?<br/>
Dados de backup são enviados toohello datacenter Olá cofre toowhich que está registrado. Olá mais fácil maneira toochange Olá datacenter toouninstall Olá agente e reinstalar o agente de saudação e registrar tooa novo cofre que pertence a toodesired datacenter.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Dá hello Azure Backup agent funciona em um servidor que usa a eliminação de duplicação do Windows Server 2012? <br/>
Sim. serviço de agente Olá converte toonormal Olá com eliminação de duplicação de dados quando ele prepara a operação de backup hello. Ele e otimiza os dados Olá para backup, criptografa dados hello e depois envia Olá criptografado dados toohello serviço de backup online.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Como alterar o local do cache Olá especificado para o agente de Backup do Azure Olá?<br/>
Local do cache Olá toochange lista a seguir de saudação de uso.

1. Pare o mecanismo de Backup Olá executando Olá comando em um prompt de comando a seguir:

    ```PS C:\> Net stop obengine``` 
  
2. Não mova os arquivos de saudação. Em vez disso, copie Olá cache espaço pasta tooa outra unidade com espaço suficiente. espaço em cache Olá original pode ser removido depois de confirmar Olá os backups estão funcionando com o novo espaço de cache hello.
3. Atualize Olá entradas do registro com a pasta de espaço do novo cache do hello caminho toohello a seguir.<br/>

    | Caminho do registro | Chave do Registro | Valor |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Novo local da pasta de cache* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Novo local da pasta de cache* |

4. Reinicie o mecanismo de Backup de saudação executando Olá comando em um prompt de comando a seguir:

    ```PS C:\> Net start obengine```

Após a criação de saudação backup for concluída com êxito no novo local de cache hello, você pode remover a pasta de cache original hello.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Onde posso colocar a pasta de cache de saudação para hello Azure Backup Agent toowork conforme o esperado?<br/>
Olá seguintes locais para a pasta de cache de saudação não são recomendadas:

* Mídia removível ou compartilhamento de rede: pasta de cache Olá deve ser o servidor de local toohello que precisa de backup usando o backup online. Não há suporte para os locais de rede ou para a mídia removível como unidades USB.
* Os Volumes offline: pasta de cache Olá deve estar online para backup esperado com o Azure Backup Agent.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Há todos os atributos da pasta de cache Olá que não têm suporte?<br/>
Hello suas combinações ou atributos a seguir não têm suporte para a pasta de cache de saudação:

* Criptografado
* Eliminação de duplicação
* Compactado
* Esparsos
* Ponto de nova análise

pasta de cache Hello e metadados de saudação VHD não tem atributos de saudação necessários para o agente de Backup do Azure hello.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Há uma quantidade de saudação tooadjust forma de largura de banda usada pelo serviço de Backup Olá?<br/>
  Sim, usar o hello **alterar propriedades** opção na largura de banda de tooadjust do hello agente de Backup. Você pode ajustar a quantidade de saudação de largura de banda e hello vezes quando você usa essa largura de banda. Para obter instruções passo a passo, consulte  **[Habilitar limitação de rede](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Gerenciar backups
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>O que acontece se eu renomear um servidor do Windows que está fazendo backup de dados tooAzure?<br/>
Ao renomear um servidor, todos os backups configurados atualmente serão interrompidos.
Registre novo nome de saudação do servidor de saudação Olá Cofre de Backup. Quando você registrar o novo nome de saudação cofre Olá, a primeira operação de backup Olá é um *completo* backup. Se precisar de dados toorecover backup cofre toohello com o nome de servidor antigo Olá, use Olá [ **outro servidor** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) opção Olá **recuperar dados** assistente.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>O que é o comprimento do caminho do hello máximo de arquivo que pode ser especificado na política de Backup usando o agente de Backup do Azure? <br/>
O agente de Backup do Azure baseia-se em NTFS. Olá [especificação de comprimento de caminho de arquivo é limitada pela API do Windows de saudação](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Se Olá arquivos tooprotect tem um comprimento de caminho de arquivo maior que o permitido pelo Olá API do Windows, faça backup de pasta pai de saudação ou unidade de disco de saudação.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Quais caracteres são permitidos no caminho de arquivo da política de Backup do Azure usando o agente de Backup do Azure? <br>
 O agente de Backup do Azure baseia-se em NTFS. Ele permite os [caracteres com suporte do NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) como parte da especificação de arquivo. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Recebo hello "Backups do Azure não foram configurados para esse servidor de" aviso, mesmo que configurei uma política de backup <br/>
Este aviso ocorre quando as configurações de agendamento de backup de saudação armazenadas no servidor de local de saudação não são Olá igual Olá configurações armazenadas no cofre de backup hello. Quando o servidor de saudação ou configurações de saudação foram recuperado tooa estado bom conhecido, agendas de backup Olá podem perder a sincronização. Se você receber esse aviso, [reconfigurar a política de backup Olá](backup-azure-manage-windows-server.md) e **executar backup agora** servidor de local de saudação tooresynchronize com o Azure.
