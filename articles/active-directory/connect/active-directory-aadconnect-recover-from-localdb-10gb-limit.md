---
title: "Conexão do AD do Azure: Como limitar toorecover do LocalDB 10GB problema | Microsoft Docs"
description: "Este tópico descreve como toorecover sincronização do Azure do AD Connect de serviço quando ele encontra LocalDB 10GB limitar o problema."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Conexão do AD do Azure: Como toorecover do limite de 10 GB do LocalDB
Conexão do AD do Azure requer um dados de identidade de toostore de banco de dados do SQL Server. Você pode usar saudação padrão do que SQL Server 2012 Express LocalDB é instalado com o Azure AD Connect ou usar seu próprio SQL completo. O SQL Server Express impõe um limite de tamanho de 10 GB. Ao usar o LocalDB e esse limite for atingido, o serviço de sincronização do Azure do AD Connect não pode iniciar ou sincronizar corretamente. Este artigo fornece as etapas de recuperação de saudação.

## <a name="symptoms"></a>Sintomas
Há dois sintomas comuns:

* Serviço de sincronização se conectar do Azure AD **está em execução** , mas falha toosynchronize com *"parado-banco de dados-disco cheio"* erro.

* Serviço de sincronização se conectar do Azure AD **é toostart não é possível**. Quando você tenta toostart serviço de hello, falhar com a mensagem de erro e de evento 6323 *"servidor de saudação encontrou um erro porque o SQL Server está sem espaço em disco."*

## <a name="short-term-recovery-steps"></a>Etapas de recuperação de curto prazo
Esta seção fornece espaço em tooreclaim DB Olá etapas necessário para a operação do serviço de sincronização se conectar do Azure AD tooresume. Olá etapas incluem:
1. [Determinar o status do serviço de sincronização Olá](#determine-the-synchronization-service-status)
2. [Reduzir Olá banco de dados](#shrink-the-database)
3. [Excluir dados de histórico de execução](#delete-run-history-data)
4. [Reduzir o período de retenção de dados de histórico de execução](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Determinar o status do serviço de sincronização Olá
Primeiro, determine se Olá serviço de sincronização ainda está executando ou não:

1. Faça logon tooyour servidor da conexão do AD do Azure como administrador.

2. Vá muito**Service Control Manager**.

3. Verificar status de saudação do **Microsoft Azure AD Sync**.


4. Se ele estiver em execução, não interromper ou reiniciar o serviço de saudação. Ignorar [banco de dados de saudação redução](#shrink-the-database) etapa e vá muito[excluir dados de histórico de execução](#delete-run-history-data) etapa.

5. Se não estiver em execução, tente toostart serviço de saudação. Se o serviço de saudação é iniciado com êxito, ignore [banco de dados de saudação redução](#shrink-the-database) etapa e vá muito[excluir dados de histórico de execução](#delete-run-history-data) etapa. Caso contrário, prossiga com [banco de dados de saudação redução](#shrink-the-database) etapa.

### <a name="shrink-hello-database"></a>Reduzir Olá banco de dados
Use toofree de operação de redução Olá backup suficiente Olá de toostart de espaço do banco de dados serviço de sincronização. Ele libera o espaço de banco de dados ao remover espaços em branco no banco de dados de saudação. Essa etapa é melhor esforço, como não há garantia de que você sempre pode recuperar espaço. toolearn mais sobre a operação de redução, leia este artigo [reduzir um banco de dados](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Ignore esta etapa se você pode obter Olá toorun de serviço de sincronização. Olá tooshrink banco de dados SQL não é recomendável porque ele pode levar toopoor desempenho devido a fragmentação tooincreased.

nome de saudação do banco de dados de saudação criado para o Azure AD Connect é **ADSync**. tooperform uma operação de redução, faça logon no como Olá sysadmin ou DBO do banco de dados de saudação. Durante a instalação do Azure AD Connect, Olá contas a seguir é concedido direitos de administrador do sistema:
* Administradores Locais
* conta de usuário de saudação que foi usado toorun AD do Azure Connect instalação.
* Olá conta de serviço de sincronização que é usada como Olá operacional contexto do serviço de sincronização se conectar do Azure AD.
* Olá grupo ADSyncAdmins que foi criado durante a instalação.

1. Saudação de banco de dados por meio da cópia de backup **ADSync.mdf** e **ADSync_log.ldf** arquivos localizados em `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` local seguro tooa.

2. Inicie uma nova sessão do PowerShell.

3. Navegue toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Iniciar **sqlcmd** utilitário executando o comando Olá `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, usando a credencial de saudação do sysadmin ou Olá DBO do banco de dados.

5. tooshrink Olá banco de dados, no prompt de sqlcmd hello (1 >), digite `DBCC Shrinkdatabase(ADSync,1);`, seguido por `GO` na próxima linha de saudação.

6. Se Olá operação for bem-sucedida, tente toostart Olá serviço de sincronização novamente. Se você puder iniciar Olá serviço de sincronização, vá muito[excluir dados de histórico de execução](#delete-run-history-data) etapa. Caso contrário, contate o Suporte.

### <a name="delete-run-history-data"></a>Excluir dados de histórico de execução
Por padrão, o Azure AD Connect retém o tooseven dias de dados de histórico de execução. Nesta etapa, excluímos Olá espaço de tooreclaim banco de dados de dados de histórico de execução para que o serviço de sincronização se conectar do Azure AD pode começar a sincronizar novamente.

1.  Iniciar **Synchronization Service Manager** pelo vai tooSTART → serviço de sincronização.

2.  Vá toohello **operações** guia.

3.  Em **Ações**, selecione **Limpar Execuções**…

4.  Você pode escolher a opção **Limpar todas as execuções** ou **Limpar execuções antes de... <date>**. É recomendável que você comece desmarcando os dados de histórico de execução com mais de dois dias. Se você continuar toorun problema de tamanho do banco de dados, em seguida, escolha Olá **limpar todas as execuções** opção.

### <a name="shorten-retention-period-for-run-history-data"></a>Reduzir o período de retenção de dados de histórico de execução
Esta etapa é a probabilidade de saudação do tooreduce em execução em um problema de limite de 10 GB de saudação após vários ciclos de sincronização.

1. Abra uma nova sessão do PowerShell.

2. Execute `Get-ADSyncScheduler` e anote Olá propriedade PurgeRunHistoryInterval, que especifica o período de retenção atual hello.

3. Executar `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset Olá retenção tootwo período em dias. Ajuste o período de retenção de saudação conforme apropriado.

## <a name="long-term-solution--migrate-toofull-sql"></a>Solução de longo prazo – migrar toofull SQL
Em geral, problema de saudação é uma indicação de que o tamanho do banco de dados de 10 GB não é suficiente para toosynchronize do Azure AD Connect seu tooAzure do Active Directory local AD. É recomendável que você mude a versão completa do toousing saudação do SQL server. Diretamente, você não pode substituir Olá LocalDB de uma implantação existente do Azure AD Connect com banco de dados de saudação da versão completa de saudação do SQL. Em vez disso, você deve implantar um novo servidor do Azure AD Connect com a versão completa de saudação do SQL. É recomendável que você execute uma migração de giro onde o novo servidor de conexão do AD do Azure Olá, (com o banco de dados SQL) é implantado como um servidor de preparo, o próximo toohello existente do Azure AD Connect servidor (com LocalDB). 
* Para obter instruções sobre como tooconfigure SQL remoto com o Azure AD Connect, consulte tooarticle [instalação personalizada do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Para obter instruções sobre a migração de movimento para a atualização do Azure AD Connect, consulte tooarticle [do Azure AD Connect: atualização do toohello versão anterior mais recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
