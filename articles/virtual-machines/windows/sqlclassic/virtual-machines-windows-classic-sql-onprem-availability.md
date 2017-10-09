---
title: aaaExtend tooAzure de grupos de disponibilidade AlwaysOn local | Microsoft Docs
description: "Este tutorial usa recursos criados com o modelo de implantação clássico hello e descreve como toouse Olá assistente Adicionar réplica no SQL Server Management Studio (SSMS) tooadd uma réplica do grupo de disponibilidade AlwaysOn no Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Estender tooAzure de grupos de disponibilidade AlwaysOn no local
Os grupos de disponibilidade AlwaysOn fornecem alta disponibilidade para grupos de bancos de dados adicionando réplicas secundárias. Essas réplicas permitem o failover dos bancos de dados em caso de falha. Além disso, eles podem ser usado toooffload ler cargas de trabalho ou tarefas de backup.

Você pode estender tooMicrosoft de grupos de disponibilidade local do Azure, o provisionamento de um ou mais máquinas virtuais do Azure com o SQL Server e, em seguida, adicioná-los como réplicas tooyour grupos de disponibilidade local.

Este tutorial pressupõe que você ter Olá seguinte:

* Uma assinatura ativa do Azure. Você pode [se inscrever para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um grupo de disponibilidade AlwaysOn local existente. Para obter mais informações sobre os grupos de disponibilidade, consulte [Grupos de disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).
* Conectividade entre hello no local de rede e sua rede virtual do Azure. Para obter mais informações sobre como criar essa rede virtual, consulte [criar uma Site a Site conexão usando Olá portal do Azure (clássica)](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="add-azure-replica-wizard"></a>Assistente de adição de réplica do Azure
Esta seção mostra como Olá toouse **assistente Adicionar réplica do Azure** tooextend sua solução de grupo de disponibilidade AlwaysOn tooinclude Azure réplicas.

> [!IMPORTANT]
> Olá **assistente Adicionar réplica do Azure** só oferece suporte a máquinas virtuais criadas com o modelo de implantação clássico hello. Novas implantações de VM devem usar o modelo de Gerenciador de recursos mais recente da saudação. Se você estiver usando máquinas virtuais com o Gerenciador de recursos, em seguida, você deve adicionar manualmente a réplica do Azure secundária hello usando Transact-SQL commmands (não mostrados aqui). Este assistente não funcionará no cenário do Gerenciador de recursos de saudação.

1. De dentro do SQL Server Management Studio, expanda **Alta Disponibilidade AlwaysOn** > **Grupos de Disponibilidade** > **[Nome do seu Grupo de Disponibilidade]**.
2. Clique com o botão direito em **Réplicas da Disponibilidade**, em seguida, clique em **Adicionar Réplica**.
3. Por padrão, Olá **tooAvailability réplica Adicionar Assistente de grupo** é exibido. Clique em **Avançar**.  Se você tiver selecionado Olá **não mostrar esta página novamente** opção final Olá Olá página durante uma inicialização anterior deste assistente, esta tela não será exibida.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Será necessário tooconnect tooall réplicas secundárias existentes. Você pode clicar em **Conectar...** ao lado de cada réplica ou pode clicar em **Conectar Tudo...** na parte inferior de saudação da tela hello. Após a autenticação, clique em **próximo** tooadvance toohello próxima tela.
5. Em Olá **especificar réplicas** página, várias guias são listados na parte superior da saudação: **réplicas**, **pontos de extremidade**, **preferências de Backup**, e **Ouvinte**. De saudação **réplicas** , clique em **adicionar réplica do Azure...** toolaunch Olá assistente Adicionar réplica do Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Selecione um certificado de gerenciamento do Azure existente do repositório de certificados do Windows local Olá se você tiver instalado uma antes. Selecione ou insira a id de saudação de uma assinatura do Azure se você tiver usado uma antes. Você pode clicar toodownload de Download e, em seguida, instale um certificado de gerenciamento do Azure e baixar Olá lista de assinaturas usando uma conta do Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Você populará cada campo na página de saudação com valores que serão usados toocreate Olá Máquina Virtual (VM) do Azure que hospedará a réplica de saudação.
   
   | Configuração | Descrição |
   | --- | --- |
   | **Imagem** |Selecionar a combinação de saudação desejada do sistema operacional e do SQL Server |
   | **Tamanho da MV** |Selecione Olá tamanho da VM que melhor atenda às suas necessidades de negócios |
   | **Nome da VM** |Especifique um nome exclusivo para Olá nova VM. Olá nome deve conter entre 3 e 15 caracteres, pode conter apenas letras, números e hifens e deve começar com uma letra e terminar com uma letra ou um número. |
   | **Nome de usuário da VM** |Especifique um nome de usuário que se tornará a conta de administrador Olá Olá VM |
   | **Senha do administrador da VM** |Especifique uma senha para a nova conta de saudação |
   | **Confirmar Senha** |Confirmar senha Olá de nova conta de saudação |
   | **Rede Virtual** |Especifique a saudação que Olá nova VM deve usar de rede virtual do Azure. Para obter mais informações sobre redes virtuais, consulte [Visão Geral da Rede Virtual](../../../virtual-network/virtual-networks-overview.md). |
   | **Sub-rede da rede virtual** |Especifique a sub-rede da rede virtual Olá que Olá que nova VM deve usar |
   | **Domínio** |Confirmar valor preenchida previamente Olá domínio hello está correta |
   | **Nome de usuário do domínio** |Especifique uma conta que está no grupo de administradores locais Olá em nós de cluster local Olá |
   | **Senha** |Especifique a senha Olá para o nome de usuário de domínio Olá |
8. Clique em **Okey** toovalidate configurações de implantação de saudação.
9. Os termos legais são exibidos em seguida. Leia e clique em **Okey** se concordar toothese termos.
10. Olá **especificar réplicas** página é exibida novamente. Verifique as configurações de saudação para nova réplica do Azure Olá em Olá **réplicas**, **pontos de extremidade**, e **preferências de Backup** guias. Modificar configurações toomeet seus requisitos de negócios.  Para obter mais informações sobre parâmetros de saudação contidos nessas guias, consulte [especificar página de réplicas (nova disponibilidade grupo assistente/Assistente Adicionar réplica)](https://msdn.microsoft.com/library/hh213088.aspx). Observe que ouvintes não podem ser criados usando a guia de ouvinte Olá para grupos de disponibilidade que contêm réplicas do Azure. Além disso, se um ouvinte já tiver sido criado Olá toolaunching anterior assistente, você receberá uma mensagem indicando que não há suporte no Azure. Vamos examinar como toocreate ouvintes no hello **criar um ouvinte de grupo de disponibilidade** seção.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Clique em **Avançar**.
12. Selecionar método de sincronização de dados Olá deseja toouse em Olá **selecionar sincronização de dados inicial** página e clique em **próximo**. Na maioria dos cenários, selecione **Sincronização Completa de Dados**. Para obter mais informações sobre métodos de sincronização de dados, consulte [Selecionar a página Sincronização de Dados Inicial (assistentes de grupo de disponibilidade AlwaysOn)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Analisar resultados Olá Olá **validação** página. Corrija questões pendentes e execute novamente a validação de saudação se necessário. Clique em **Avançar**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Revisar configurações Olá Olá **resumo** página e, em seguida, clique em **concluir**.
15. processo de provisionamento de saudação começa. Quando o Assistente de saudação for concluído com êxito, clique em **fechar** tooexit fora do Assistente de saudação.

> [!NOTE]
> Olá assistente Adicionar réplica do Azure cria um arquivo de log em Users\User Name\AppData\Local\SQL Server\AddReplicaWizard. Esse arquivo de log pode ser usado tootroubleshoot falhado implantações de réplica do Azure. Se Olá Assistente falhar ao executar qualquer ação, todas as operações anteriores são revertidas, incluindo a exclusão Olá provisionado a VM.
> 
> 

## <a name="create-an-availability-group-listener"></a>Criar um ouvinte de grupo de disponibilidade
Depois que o grupo de disponibilidade Olá tiver sido criado, você deve criar um ouvinte para clientes tooconnect toohello réplicas. Os ouvintes direcionam entrada hello de tooeither conexões primária ou uma réplica secundária somente leitura. Para obter mais informações sobre os ouvintes, consulte [Configurar um ouvinte de ILB para os Grupos de Disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Próximas etapas
Na saudação de toousing adição **assistente Adicionar réplica do Azure** tooextend tooAzure o grupo de disponibilidade AlwaysOn, você também pode mover algumas cargas de trabalho do SQL Server tooAzure completamente. tooget iniciado, consulte [provisionar uma máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

