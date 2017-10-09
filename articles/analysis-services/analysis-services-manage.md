---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Saiba como toomanage um Analysis Services server no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Gerenciar o Analysis Services
Depois de criar um servidor do Analysis Services no Azure, pode haver algumas tarefas de administração, você precisa tooperform imediatamente ou em trânsito de saudação algum tempo para baixo. Por exemplo, execute o processamento toohello de atualização de dados, controlar quem pode acessar os modelos de saudação do servidor ou monitorar a integridade do servidor. Algumas tarefas de gerenciamento só podem ser executadas no Portal do Azure, outras no SQL Server Management Studio (SSMS) e algumas tarefas podem ser executadas em ambos.

## <a name="azure-portal"></a>Portal do Azure
[Portal do Azure](http://portal.azure.com/) é onde você pode criar e excluir servidores, monitorar os recursos do servidor, alterar o tamanho e gerenciar o acesso tooyour servidores.  Se você estiver enfrentando problemas, também poderá enviar uma solicitação de suporte.

![Obter o nome do servidor no Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Conectando o servidor tooyour no Azure é como conectar-se a instância de servidor tooa em sua própria organização. No SSMS, você pode executar muitas das Olá mesmo tarefas como processar dados ou criar um script de processamento, gerenciar funções e usar o PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Baixar e instalar o SSMS
tooget todos Olá experiência mais suave hello e recursos mais recentes ao conectar-se o servidor de serviços de análise do Azure tooyour, certifique-se de que você está usando a versão mais recente de saudação do SSMS. 

[Baixar o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect com SSMS
 Ao usar o SSMS, antes de saudação do servidor conectado tooyour primeira vez, verifique se que seu nome de usuário está incluído no grupo de administradores de serviços de análise de saudação. mais, consulte toolearn [os administradores de servidor](#server-administrators) posteriormente neste artigo.

1. Antes de você se conectar, é necessário tooget nome do servidor de saudação. Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome do servidor de saudação de cópia.
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. No SSMS > **Pesquisador de Objetos**, clique em **Conectar** > **Analysis Services**.
3. Em Olá **conectar tooServer** colar em nome do servidor de saudação, em seguida, na caixa de diálogo **autenticação**, escolha um dos seguintes tipos de autenticação de saudação:
   
    **Autenticação do Windows** toouse suas credenciais de domínio ome de usuário e senha do Windows.

    **A autenticação de senha do Active Directory** toouse uma conta organizacional. Por exemplo, ao conectar-se de um computador que não ingressou em um domínio.

    **Autenticação do Active Directory Universal** toouse [autenticação multifator ou não interativo](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Conectar-se no SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Administradores de servidor e usuários de banco de dados
Nos Azure Analysis Services, há dois tipos de usuários, administradores de servidor e usuários de banco de dados. Os dois tipos de usuários devem estar no Azure Active Directory e devem ser especificados por endereços de email organizacionais ou UPN. mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Solucionar problemas de conexão
Ao se conectar usando o SSMS, se você tiver problemas, talvez seja necessário tooclear cache de logon de saudação. Nada é armazenado em cache toodisc. tooclear Olá de cache, feche e reinicialização Olá conectam processo. 

## <a name="next-steps"></a>Próximas etapas
Se você já não tiver implantado um novo servidor de modelo de tabela tooyour, agora é um bom momento. mais, consulte toolearn [implantar serviços de análise de tooAzure](analysis-services-deploy.md).

Se você implantou um servidor de tooyour de modelo, você está pronto tooconnect tooit usando um cliente ou navegador. mais, consulte toolearn [obter dados do servidor do Azure Analysis Services](analysis-services-connect.md).

