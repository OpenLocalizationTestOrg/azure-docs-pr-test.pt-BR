---
title: 'Backup do Azure: backups consistentes com o aplicativo de VMs Linux | Microsoft Docs'
description: "Use scripts tooguarantee backups consistentes com aplicativos tooAzure, para as máquinas virtuais de Linux. scripts de saudação aplicam-se apenas tooLinux VMs em uma implantação do Gerenciador de recursos; scripts de saudação não se aplicam tooWindows VMs ou implantações do service manager. Este artigo descreve as etapas de saudação para configurar scripts de hello, incluindo a solução de problemas."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: backup consistente com o aplicativo; backup de VM do Azure consistente com o aplicativo; Backup de VM Linux; Backup do Azure
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Backup consistente com o aplicativo de VMs Linux do Azure (versão prévia)

Este artigo aborda Olá pré-script Linux e do framework de pós- script e como ela pode ser backups consistentes com aplicativos de tootake usada das VMs do Linux do Azure.

> [!Note]
> estrutura de script de pré e pós-Olá tem suporte somente para máquinas virtuais Linux implantadas pelo Gerenciador de recursos do Azure. Não há suporte a scripts para consistência com aplicativos em máquinas virtuais implantadas pelo Service Manager ou máquinas virtuais do Windows.
>

## <a name="how-hello-framework-works"></a>Como funciona o framework Olá

estrutura Olá fornece uma opção toorun pré-scripts de personalizados e pós-scripts enquanto faz instantâneos VM. Pré-scripts são executados apenas antes de tirar instantâneo VM hello e pós-os scripts são executados imediatamente depois de tirar instantâneo VM hello. Isso proporciona Olá flexibilidade toocontrol seu ambiente e o aplicativo enquanto faz instantâneos VM.

Nesse cenário, é importante tooensure consistente com o aplicativo backup de VM. pré-script de Olá pode invocar o aplicativo nativo APIs tooquiesce Olá IOs e liberar o disco toohello conteúdo na memória. Isso garante que esse Instantâneo Olá é consistente com o aplicativo (ou seja, o aplicativo hello vem quando pós-restauração Olá VM é inicializada). Pós-script pode ser usado toothaw Olá IOs. Ele faz isso por meio de APIs de aplicativo nativo para que o aplicativo hello pode retomar o instantâneo de VM de postagem de operações normais.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Etapas tooconfigure script de pré e pós-

1. Faça logon no hello raiz usuário toohello VM do Linux que você deseja tooback backup.

2. Baixar **VMSnapshotScriptPluginConfig.json** de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)e, em seguida, copie-o toohello **/etc/azure** pasta em todas as VMs de saudação que você vai tooback backup. Criar hello **/etc/azure** diretório se ele já não existe.

3. Copie Olá script de pré e pós-para o aplicativo no hello todas as máquinas virtuais que você planejar tooback backup. Você pode copiar tooany local scripts Olá Olá VM. Ser tooupdate se Olá caminho completo Olá arquivos de script na Olá **VMSnapshotScriptPluginConfig.json** arquivo.

4. Certifique-se de saudação as seguintes permissões para esses arquivos:

   - **VMSnapshotScriptPluginConfig.json**: permissão “600.” Por exemplo, apenas o usuário "raiz" deve ter um arquivo de toothis de permissões de "leitura" e "gravação" e nenhum usuário deve ter permissões de "execução".

   - **Arquivo de pré-script**: permissão "700".  Por exemplo, apenas o usuário "raiz" deve ter "leitura", "gravação" e "executar" arquivo de toothis de permissões.
  
   - **Pós-script** permissão "700". Por exemplo, apenas o usuário "raiz" deve ter "leitura", "gravação" e "executar" arquivo de toothis de permissões.

   > [!Important]
   > estrutura Olá fornece aos usuários uma grande quantidade de energia. É importante que é seguro e o usuário "raiz" só tem acesso toocritical JSON e arquivos de script.
   > Se os requisitos de saudação anteriores não forem atendidos, Olá script não é executado. Isso resulta em backup consistente de sistema de arquivos/falha.
   >

5. Configure o **VMSnapshotScriptPluginConfig.json** conforme descrito aqui:
    - **pluginName**: deixe esse campo como está ou os scripts podem não funcionar conforme o esperado.

    - **preScriptLocation**: fornecer o caminho completo de saudação do pré-script de Olá em Olá VM toobe do que será feito backup.

    - **postScriptLocation**: fornecer o caminho completo de saudação do pós-script Olá em Olá VM toobe do que será feito backup.

    - **preScriptParams**: fornecem parâmetros opcionais de saudação que precisam toobe passado pré-script toohello. Todos os parâmetros deverão estar entre aspas e deverão ser separados por vírgulas se houver vários parâmetros.

    - **postScriptParams**: fornecer parâmetros opcionais de saudação que precisam toobe passado pós-script toohello. Todos os parâmetros deverão estar entre aspas e deverão ser separados por vírgulas se houver vários parâmetros.

    - **preScriptNoOfRetries**: definir Olá número de vezes que deve ser repetida pré-script Olá, se houver algum erro antes de encerrar. Zero significa apenas uma tentativa e nenhuma repetição se houver uma falha.

    - **postScriptNoOfRetries**: definir Olá número de vezes que deve ser repetida pós-script Olá, se houver algum erro antes de encerrar. Zero significa apenas uma tentativa e nenhuma repetição se houver uma falha.
    
    - **timeoutInSeconds**: especificar tempos limites individuais para pré-script de Olá e Olá pós.

    - **continueBackupOnFailure**: Defina esse valor muito**true** se deseja Azure Backup toofall tooa back sistema consistente/falha consistente backup de arquivo se script pré ou pós-script falha. Essa configuração muito**false** falhar Olá backup no caso de falha de script (exceto quando você tem em um único disco VM que vão o backup novamente toocrash consistente, independentemente dessa configuração).

    - **fsFreezeEnabled**: Especifique se fsfreeze Linux deve ser chamado enquanto você está fazendo a consistência do sistema de arquivos tooensure Olá VM instantâneo. É recomendável manter essa configuração definida muito**true** , a menos que seu aplicativo tem uma dependência em Desabilitar fsfreeze.

6. estrutura do script Hello agora está configurada. Se o backup de VM Olá já estiver configurado, o próximo backup de saudação invoca scripts hello e dispara backup consistente com o aplicativo. Se o backup de VM Olá não estiver configurado, configure-o usando [máquinas virtuais do Azure tooRecovery serviços cofres de backup.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Solucionar problemas

Verifique se você adicionar log apropriadas ao gravar o script de pré e pós- e revisar os problemas de script de sua toofix de logs do script. Se você ainda tiver problemas ao executar scripts, consulte toohello para obter mais informações a tabela a seguir.

| Erro | Mensagem de erro | Ação recomendada |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |pré-script de Olá retornou um erro, para que o backup pode não ser consistente com o aplicativo. | Examine os logs de falha de saudação para seu problema de saudação do script toofix.|  
|   Post-ScriptExecutionFailed |    pós-script Olá retornou um erro que pode afetar o estado do aplicativo. |  Examine logs de falha de saudação para seu problema de saudação do script toofix e verificar o estado do aplicativo hello. |
| Pre-ScriptNotFound |  Olá pré-script não foi encontrado no local de saudação que é especificado no hello **VMSnapshotScriptPluginConfig.json** arquivo de configuração. | Certifique-se que pré-script está presente no caminho de saudação especificado no hello config tooensure consistente com o aplicativo o backup do arquivo.|
| Post-ScriptNotFound | Olá pós-script não foi encontrado no local de saudação que é especificado no hello **VMSnapshotScriptPluginConfig.json** arquivo de configuração. | Certifique-se que pós-script está presente no caminho de saudação especificado no hello config tooensure consistente com o aplicativo o backup do arquivo.|
| IncorrectPluginhostFile | Olá **Pluginhost** arquivo, o que vem com hello extensão VmSnapshotLinux, está corrompido, portanto, não é possível executar o script de pré e pós- e backup Olá não será consistente com o aplicativo.   | Desinstalar Olá **VmSnapshotLinux** extensão e ele serão reinstalado automaticamente com o problema do hello próximo backup toofix Olá. |
| IncorrectJSONConfigFile | Olá **VMSnapshotScriptPluginConfig.json** arquivo está incorreta, portanto pré-script e pós-script não é possível executar e backup Olá não será consistente com o aplicativo. | Baixar a cópia de saudação do [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) e configurá-lo novamente. |
| InsufficientPermissionforPre-Script | Para executar scripts, usuário "raiz" deve ser o proprietário de saudação do arquivo hello e arquivo hello deve ter permissões "700" (ou seja, apenas "proprietário" deve ter "leitura", "gravação" e "executar" permissões). | Verifique se é de usuário "raiz" hello "proprietário" hello do arquivo de script e que somente "proprietário" tem "permissões de leitura", "gravação" e "executar". |
| InsufficientPermissionforPost-Script | Para executar scripts, usuário raiz deve ser o proprietário de saudação do arquivo hello e arquivo hello deve ter permissões "700" (ou seja, apenas "proprietário" deve ter "leitura", "gravação" e "executar" permissões). | Verifique se é de usuário "raiz" hello "proprietário" hello do arquivo de script e que somente "proprietário" tem "permissões de leitura", "gravação" e "executar". |
| Pre-ScriptTimeout | Olá a execução do pré-script de backup consistente com o aplicativo hello atingiu o tempo limite. | Verifique o script hello e aumentar o tempo limite de saudação em Olá **VMSnapshotScriptPluginConfig.json** arquivo está localizado em **/etc/azure**. |
| Post-ScriptTimeout | a execução do pós-script de backup consistente com o aplicativo hello Olá atingiu o tempo limite. | Verifique o script hello e aumentar o tempo limite de saudação em Olá **VMSnapshotScriptPluginConfig.json** arquivo está localizado em **/etc/azure**. |

## <a name="next-steps"></a>Próximas etapas
[Configurar o Cofre de serviços de recuperação de backup tooa VM](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
