---
title: "aaaSecurity recursos toohelp proteger backups híbridos que usam o Backup do Azure | Microsoft Docs"
description: "Saiba como os recursos de segurança toouse nos backups de toomake de Backup do Azure mais seguros"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Toohelp de recursos de segurança proteger backups híbridos que usam o Backup do Azure
Preocupações sobre problemas de segurança, como malware, ransomware e invasão, estão aumentando. Esses problemas de segurança podem ser dispendiosos em termos de dinheiro e dados. tooguard contra tais ataques, o Backup do Azure agora oferece segurança recursos toohelp proteger backups híbrida. Este artigo aborda como tooenable e usar esses recursos, usando um agente de serviços de recuperação do Azure e o Azure Backup Server. Esses recursos incluem:

- **Prevenção**. Uma camada adicional de autenticação será adicionada sempre que uma operação crítica, como a alteração de senha, for executada. Essa validação é tooensure que essas operações podem ser executadas apenas por usuários com credenciais do Azure válidas.
- **Alertas**. Uma notificação por email é enviada a administração de assinatura toohello sempre que uma operação crítica como a exclusão de dados de backup é executada. Este email garante que o usuário Olá é notificado rapidamente sobre essas ações.
- **Recuperação**. Dados de backup excluídos são mantidos por mais de 14 dias da data de saudação da exclusão de saudação. Isso garante a capacidade de recuperação de dados de saudação dentro de um determinado período de tempo, portanto não há nenhuma perda de dados, mesmo se um ataque acontece. Além disso, um número maior de pontos de recuperação mínima é mantido tooguard contra dados corrompidos.

> [!NOTE]
> Os recursos de segurança não devem ser habilitados se você estiver usando a infraestrutura como um serviço (IaaS) do backup da VM. Esses recursos ainda não estão disponíveis para o backup de VM do IaaS e, portanto, habilitá-los não terá qualquer impacto. Os recursos de segurança só deverão ser habilitados se você estiver usando: <br/>
>  * **Agente de Backup do Azure**. Versão mínima do agente 2.0.9052. Depois de habilitar esses recursos, você deve atualizar operações críticas do toothis agent versão tooperform. <br/>
>  * **Servidor de Backup do Azure**. Versão mínima do agente de Backup do Azure 2.0.9052 com o Servidor de Backup do Azure atualização 1. <br/>
>  * **System Center Data Protection Manager**. Versão mínima do agente de Backup do Azure 2.0.9052 com o Data Protection Manager 2012 R2 UR12 ou Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Esses recursos estão disponíveis somente para o cofre dos Serviços de Recuperação. Todos os Olá recém-criado cofres dos serviços de recuperação ter esses recursos habilitados por padrão. Para cofres de serviços de recuperação existentes, os usuários habilitar esses recursos usando as etapas Olá mencionadas Olá seção a seguir. Depois de Olá recursos estão habilitados, eles se aplicam tooall computadores de agente de serviços de recuperação de saudação, instâncias de servidor de Backup do Azure e servidores do Data Protection Manager registrados no cofre de saudação. Habilitar essa configuração é uma ação única e você não poderá desabilitar esses recursos depois de habilitá-los.
>

## <a name="enable-security-features"></a>Habilitar recursos de segurança
Se você estiver criando um cofre de serviços de recuperação, você pode usar todos os recursos de segurança de saudação. Se você estiver trabalhando com um cofre existente, habilite os recursos de segurança executando estas etapas:

1. Entre no toohello portal do Azure usando suas credenciais do Azure.
2. Selecione **Procurar** e digite **Serviços de Recuperação**.

    ![Captura de tela da opção Procurar no portal do Azure](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    saudação de lista de cofres de serviços de recuperação é exibida. Nesta lista, selecione um cofre. painel do cofre selecionado Olá é aberto.
3. Na lista de saudação de itens que aparece no cofre de saudação em **configurações**, clique em **propriedades**.

    ![Captura de tela das opções do cofre dos Serviços de Recuperação](./media/backup-azure-security-feature/vault-list-properties.png)
4. Em **Configurações de Segurança**, clique em **Atualizar**.

    ![Captura de tela das propriedades do cofre dos Serviços de Recuperação](./media/backup-azure-security-feature/security-settings-update.png)

    link de atualização Hello abre Olá **as configurações de segurança** folha, que fornece um resumo dos recursos de saudação e permite que você habilitá-los.
5. Na lista suspensa de saudação **tiver configurado o Azure multi-Factor Authentication?**, selecione um valor tooconfirm se você tiver habilitado [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md). Se estiver habilitado, você deverá tooauthenticate de outro dispositivo (por exemplo, um telefone celular) ao entrar toohello portal do Azure.

   Quando você realiza operações críticas no Backup, você tem tooenter um PIN, disponível no portal do Azure de saudação de segurança. A habilitação da Autenticação Multifator do Azure adiciona uma camada de segurança. Somente usuários com credenciais do Azure válidas e autenticadas de um segundo dispositivo, pode acessar Olá portal do Azure.
6. Selecione configurações de segurança de toosave **habilitar** e clique em **salvar**. Você pode selecionar **habilitar** somente depois que você selecione um valor de saudação **tiver configurado o Azure multi-Factor Authentication?** lista na etapa anterior hello.

    ![Captura de tela das configurações de segurança](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Recuperar dados de backup excluídos
Backup retém dados de backup excluídos por mais 14 dias e não é excluído imediatamente se hello **parar backup com dados de backup delete** operação é executada. toorestore esses dados no período de 14 dias hello, levar Olá etapas, dependendo se você estiver usando a seguir:

Para usuários do **Agente de Serviços de Recuperação do Azure**:

1. Se o computador Olá onde os backups foram acontecendo ainda está disponível, use [recuperar dados toohello mesma máquina](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) nos serviços de recuperação do Azure, toorecover de todos os pontos de recuperação antigos hello.
2. Se este computador não estiver disponível, use [recuperar tooan alternativa máquina](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse tooget de computador dos serviços de recuperação do Azure outro esses dados.

Para usuários do **Servidor de Backup do Azure**:

1. Se o servidor de saudação onde os backups foram acontecendo ainda está disponível, proteger novamente Olá excluída fontes de dados e usar Olá **recuperar dados** toorecover de todos os pontos de recuperação antigos Olá de recursos.
2. Se esse servidor não estiver disponível, use [recuperar dados de outro servidor de Backup do Azure](backup-azure-alternate-dpm-server.md) toouse tooget da instância do servidor de Backup do Azure outro esses dados.

Para usuários do **Data Protection Manager**:

1. Se o servidor de saudação onde os backups foram acontecendo ainda está disponível, proteger novamente Olá excluída fontes de dados e usar Olá **recuperar dados** toorecover de todos os pontos de recuperação antigos Olá de recursos.
2. Se esse servidor não estiver disponível, use [adicionar DPM externo](backup-azure-alternate-dpm-server.md) toouse outro tooget de servidor do Data Protection Manager esses dados.

## <a name="prevent-attacks"></a>Impedir ataques
As verificações foram adicionadas toomake-se de que apenas usuários válidos podem executar várias operações. Isso inclui a adição de uma camada extra de autenticação, e a manutenção de um período de retenção mínimo para fins de recuperação.

### <a name="authentication-tooperform-critical-operations"></a>Operações críticas de tooperform de autenticação
Como parte da adição de uma camada extra de autenticação para operações críticas, são solicitada tooenter um PIN de segurança quando você executar **parar proteção com dados de exclusão** e **alterar senha** operações .

tooreceive esse PIN:

1. Entrar toohello portal do Azure.
2. Procurar muito**Cofre de serviços de recuperação** > **configurações** > **propriedades**.
3. Em **PIN de Segurança**, clique em **Gerar**. Isso abrirá uma folha que contém a saudação PIN toobe inserido na interface de usuário de agente de serviços de recuperação do Azure hello.
    Esse PIN é válido somente por cinco minutos e é gerado automaticamente após esse período.

### <a name="maintain-a-minimum-retention-range"></a>Manter um intervalo de retenção mínimo
pontos de tooensure que sempre há um número válido de recuperação disponíveis, Olá verificações a seguir foram adicionado:

- Para a retenção diária, é necessário no mínimo **sete** dias de retenção.
- Para a retenção semanal, é necessário no mínimo **quatro** semanas de retenção.
- Para a retenção mensal, é necessário no mínimo **três** meses de retenção.
- Para a retenção anual, é necessário no mínimo **um** ano de retenção.

## <a name="notifications-for-critical-operations"></a>Notificações para operações críticas
Normalmente, quando é executada uma operação crítica, Olá administrador de assinatura é enviada uma notificação por email com detalhes sobre a operação de saudação. Você pode configurar os destinatários de email adicionais para essas notificações usando Olá portal do Azure.

recursos de segurança Olá mencionados neste artigo fornecem mecanismos de defesa contra ataques direcionados. Além disso, se ocorrer um ataque, esses recursos oferecem Olá capacidade toorecover seus dados.

## <a name="troubleshooting-errors"></a>Solucionar erros
| Operação | Detalhes do erro | Resolução |
| --- | --- | --- |
| Alteração da política |não foi possível modificar a política de backup Hello. Erro: falha da operação atual de saudação devido a erro de serviço interno tooan [0x29834]. Repita a operação Olá após algum tempo. Se Olá problema persistir, entre em contato com o suporte da Microsoft. |**Causa:**<br/>Esse erro ocorre quando as configurações de segurança estiverem habilitadas, tente o período de retenção tooreduce abaixo dos valores mínimo Olá especificado acima e são versão sem suporte (versões com suporte são especificadas na primeira anotação deste artigo). <br/>**Ação recomendada:**<br/> Nesse caso, você deve definir o período de retenção acima Olá mínimo de retenção período especificado (sete dias para o diário, quatro semanas para semanal, três semanas para o mensal ou um ano para o anual) tooproceed com a política relacionadas a atualizações. Opcionalmente, a abordagem preferencial seria tooupdate agente de backup, tooleverage de servidor de Backup do Azure e/ou o DPM UR todas Olá atualizações de segurança. |
| Alterar frase secreta |O PIN de Segurança inserido está incorreto. (ID: 100130) Fornece toocomplete de PIN de segurança correto Olá esta operação. |**Causa:**<br/> Esse erro ocorre quando você insere um PIN de Segurança inválido ou expirado ao executar uma operação crítica (como alteração da frase secreta). <br/>**Ação recomendada:**<br/> operação de saudação toocomplete, você deve inserir o PIN de segurança válido. tooget Olá PIN, faça logon no portal de tooAzure e navegue Cofre de serviços tooRecovery > Configurações > Propriedades > Gerar PIN de segurança. Use essa frase secreta toochange PIN. |
| Alterar frase secreta |Falha na operação. ID: 120002 |**Causa:**<br/>Esse erro surge quando as configurações de segurança estiverem habilitadas, tente toochange senha e você estiver usando a versão sem suporte (versões válidas especificadas na primeira anotação deste artigo).<br/>**Ação recomendada:**<br/> frase secreta toochange, primeiro atualize versão do agente de backup toominimum 2.0.9052 mínimo, o Azure Backup server toominimum atualização 1 e/ou o DPM toominimum UR12 do DPM 2012 R2 ou o DPM 2016 UR2 (download links abaixo), em seguida, insira o PIN de segurança válido. tooget Olá PIN, faça logon no portal de tooAzure e navegue Cofre de serviços tooRecovery > Configurações > Propriedades > Gerar PIN de segurança. Use essa frase secreta toochange PIN. |

## <a name="next-steps"></a>Próximas etapas
* [Introdução ao Cofre de serviços de recuperação do Azure](backup-azure-vms-first-look-arm.md) tooenable esses recursos.
* [Baixar o agente de serviços de recuperação do Azure mais recente Olá](http://aka.ms/azurebackup_agent) toohelp proteger computadores Windows e proteger seus dados contra ataques de backup.
* [Download Olá servidor de Backup mais recente do Azure](https://aka.ms/latest_azurebackupserver) toohelp proteger cargas de trabalho e proteger seus dados contra ataques de backup.
* [Baixar UR12 para o System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) ou [baixar UR2 para o Data Protection Manager do System Center 2016](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp proteger cargas de trabalho e proteger seus dados contra ataques de backup.
