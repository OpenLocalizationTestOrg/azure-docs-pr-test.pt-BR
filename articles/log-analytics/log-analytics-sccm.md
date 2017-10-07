---
title: "aaaConnect análise do Configuration Manager tooLog | Microsoft Docs"
description: "Este artigo mostra Olá etapas tooconnect tooLog do Configuration Manager, análise e iniciar a análise de dados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Conectar-se a análise de tooLog do Configuration Manager
Você pode conectar o System Center Configuration Manager tooLog análise em dados de coleção de dispositivo de toosync do OMS. Isso disponibiliza dados da hierarquia do Configuration Manager no OMS.

## <a name="prerequisites"></a>Pré-requisitos

O Log Analytics dá suporte à ramificação atual do System Center Configuration Manager, versão 1606 e superior.  

## <a name="configuration-overview"></a>Visão geral de configuração
Olá, as etapas a seguir resume Olá processo tooconnect análise tooLog do Configuration Manager.  

1. No Portal de gerenciamento do hello, registrar o Configuration Manager como um aplicativo Web e/ou API da Web do aplicativo e garantir que você tenha Olá cliente e ID de chave secreta do cliente de registro de saudação do Active Directory do Azure. Consulte [usar o aplicativo do portal toocreate do Active Directory e a entidade de serviço que pode acessar recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md) para obter informações detalhadas sobre como executar essa etapa.
2. Em Olá Portal de gerenciamento do Azure, [fornecer Configuration Manager (Olá web registrado aplicativo) com permissão tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. No Configuration Manager, [adicionar uma conexão usando Olá Adicionar Assistente de Conexão de OMS](#add-an-oms-connection-to-configuration-manager).
4. No Configuration Manager, [atualizar propriedades de conexão de saudação](#update-oms-connection-properties) se Olá cliente ou a senha ou chave secreta nunca expira será perdida.
5. Com as informações do portal do OMS Olá [Baixe e instale o Microsoft Monitoring Agent de saudação](#download-and-install-the-agent) em computador de saudação com conexão de serviço do Gerenciador de configuração de saudação do ponto de função do sistema de site. Agente de saudação envia tooOMS de dados do Configuration Manager.
6. No Log Analytics, [importe coleções do Configuration Manager](#import-collections) como grupos de computadores.
7. No Log Analytics, exiba dados do Configuration Manager como [grupos de computadores](log-analytics-computer-groups.md).

Você pode ler mais sobre como conectar o Configuration Manager tooOMS em [sincronizar dados do Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Fornecer permissões tooOMS do Configuration Manager
Olá procedimento a seguir fornece Olá Portal de gerenciamento com permissões tooaccess OMS. Especificamente, você deve conceder Olá *função Colaborador* toousers no grupo de recursos de saudação em ordem tooallow Olá tooconnect do Portal de gerenciamento do Configuration Manager tooOMS.

> [!NOTE]
> Você deve especificar permissões no OMS do Configuration Manager. Caso contrário, você receberá uma mensagem de erro quando você usa o Assistente de configuração de saudação no Configuration Manager.
>
>

1. Olá abrir [portal do Azure](https://portal.azure.com/) e clique em **procurar** > **Log Analytics (OMS)** folha de análise de Log (OMS) Olá tooopen.  
2. Em Olá **Log Analytics (OMS)** folha, clique em **adicionar** tooopen Olá **espaço de trabalho do OMS** folha.  
   ![Folha do OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. Em Olá **espaço de trabalho do OMS** folha, forneça Olá informações a seguir e, em seguida, clique em **Okey**.

   * **Espaço de Trabalho do OMS**
   * **Assinatura**
   * **Grupo de recursos**
   * **Localidade**
   * **Tipo de preço**  
     ![Folha do OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > exemplo Hello acima cria um novo grupo de recursos. grupo de recursos de saudação é apenas usada tooprovide do Configuration Manager com o espaço de trabalho do OMS de toohello de permissões neste exemplo.
     >
     >
4. Clique em **procurar** > **grupos de recursos** tooopen Olá **grupos de recursos** folha.
5. Em Olá **grupos de recursos** folha, clique em grupo de recursos de saudação criado acima Olá tooopen &lt;nome do grupo de recursos&gt; folha de configurações.  
   ![folha de configurações do grupo de recursos](./media/log-analytics-sccm/sccm-azure03.png)
6. Em Olá &lt;nome do grupo de recursos&gt; folha de configurações, clique em Olá de tooopen de controle (IAM) de acesso &lt;nome do grupo de recursos&gt; folha usuários.  
   ![Folha de Usuários do grupo de recursos](./media/log-analytics-sccm/sccm-azure04.png)  
7. Em Olá &lt;nome do grupo de recursos&gt; folha de usuários, clique em **adicionar** tooopen Olá **adicionar acesso** folha.
8. Em Olá **adicionar acesso** folha, clique em **selecionar uma função**e, em seguida, selecione Olá **Colaborador** função.  
   ![selecione uma função](./media/log-analytics-sccm/sccm-azure05.png)  
9. Clique em **adicionar usuários**, selecione o usuário do Configuration Manager hello, clique em **selecione**e, em seguida, clique em **Okey**.  
   ![adicionar usuários](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Adicionar uma conexão de OMS tooConfiguration Manager
Ordem tooadd uma conexão do OMS, seu ambiente do Configuration Manager deve ter uma [ponto de conexão de serviço](https://technet.microsoft.com/library/mt627781.aspx) configurado para o modo online.

1. Em Olá **administração** espaço de trabalho do Gerenciador de configuração, selecione **conector OMS**. Isso abre o hello **Adicionar Assistente de Conexão do OMS**. Selecione **Avançar**.
2. Em Olá **geral** , confirme que você tenha feito Olá ações a seguir, e se você tiver os detalhes para cada item e selecione **próximo**.

   1. No Portal de gerenciamento de hello, você registrou o Configuration Manager como um aplicativo Web e/ou API da Web do aplicativo e que você tenha Olá [ID do cliente do registro Olá](../active-directory/active-directory-integrating-applications.md).
   2. Olá Portal de gerenciamento, você criou uma chave secreta do aplicativo para o aplicativo de saudação registrado no Active Directory do Azure.  
   3. Olá Portal de gerenciamento, você forneceu Olá web registrado aplicativo com permissão tooaccess OMS.  
      ![Página de assistente geral tooOMS Conexão](./media/log-analytics-sccm/sccm-console-general01.png)
3. Em Olá **Active Directory do Azure** tela, configure seu tooOMS de configurações de conexão, fornecendo sua **locatário** , **ID do cliente** , e **chave secreta do cliente**  , em seguida, selecione **próximo**.  
   ![Página de Assistente do Azure Active Directory de tooOMS de Conexão](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Se você realizou outros procedimentos de todos os Olá com êxito, Olá, em seguida, obter informações sobre Olá **configuração de Conexão de OMS** tela aparecerão automaticamente nesta página. Informações de configurações de conexão Olá devem ser exibido para o **assinatura do Azure** , **grupo de recursos do Azure** , e **o espaço de trabalho do Operations Management Suite**.  
   ![Página de Conexão de OMS do Assistente de tooOMS de Conexão](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Assistente de saudação se conecta toohello serviço do OMS usando informações Olá que tiver de entrada. Selecione as coleções de dispositivos Olá que você deseja toosync com o OMS e, em seguida, clique em **adicionar**.  
   ![Selecionar Coleções](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Verifique suas configurações de conexão em Olá **resumo** tela e, em seguida, selecione **próximo**. Olá **andamento** tela mostra o status de conexão hello, deve **concluir**.

> [!NOTE]
> Você deve conectar o site de nível superior do OMS toohello em sua hierarquia. Se você conectar o OMS tooa um site primário autônomo e, em seguida, adicionar um ambiente de tooyour do site de administração central, você será toodelete e recrie a conexão de OMS Olá na nova hierarquia de saudação.
>
>

Depois de vincular tooOMS do Configuration Manager, você pode adicionar ou remover coleções e exibir propriedades de saudação do hello conexão do OMS.

## <a name="update-oms-connection-properties"></a>Atualizar as propriedades da conexão do OMS
Se uma chave de segredo do cliente ou a senha nunca expira ou perdida, você precisará de propriedades de conexão de OMS do toomanually atualização hello.

1. No Configuration Manager, navegue muito**serviços de nuvem** , em seguida, selecione **conector OMS** tooopen Olá **propriedades de Conexão de OMS** página.
2. Nessa página, clique em Olá **Active Directory do Azure** guia tooview seu **locatário**, **ID do cliente**, **expiração chave secreta do cliente**. **Verifique se** sua **Chave secreta do cliente** caso ela tenha expirado.

## <a name="download-and-install-hello-agent"></a>Baixe e instale o agente de saudação
1. No portal do OMS hello, [arquivo de instalação de agente de saudação de Download do OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Use uma saudação tooinstall métodos a seguir e configurar agente Olá no computador de saudação executando a função do sistema de saudação do Configuration Manager service conexão ponto de site:
   * [Instalar agente hello usando a instalação](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Instalar o agente de Olá usando a linha de comando de saudação](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Instalar o agente de saudação usando DSC na automação do Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importe coleções
Depois de ter adicionado uma conexão de OMS tooConfiguration Gerenciador e Olá agente instalado no computador de saudação com conexão de serviço do Gerenciador de configuração de saudação ponto de função do sistema de site, Olá próxima etapa é tooimport coleções do Configuration Manager no OMS como os grupos de computadores.

Após a importação está habilitada, informações de associação de coleção de saudação são recuperadas todos os 3 horas tookeep Olá associações de coleção atuais. Você pode escolher a importação de toodisable a qualquer momento.

1. No portal do OMS hello, clique em **configurações**.
2. Clique em Olá **grupos de computadores** guia e, em seguida, clique em Olá **SCCM** guia.
3. Selecione **Importar associações de coleta do Configuration Manager** e clique em **Salvar**.  
   ![Grupos de computadores – guia SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Exibir dados do Configuration Manager
Depois que você adicionou uma conexão de OMS tooConfiguration Gerenciador e instalado agente Olá no computador de saudação executando a função do sistema de saudação do Configuration Manager service conexão ponto de site, os dados do agente de saudação são enviados tooOMS. No OMS, suas coleções do Configuration Manager aparecem como [grupos de computadores](log-analytics-computer-groups.md). Você pode exibir grupos de saudação do hello **do Configuration Manager** página em **grupos de computadores** na **configurações**.

Após Olá coleções são importadas, você pode ver quantos computadores com associações de coleção foram detectados. Você também pode ver o número de saudação de coleções que foram importados.

![Grupos de computadores – guia SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Quando você clicar em qualquer um, abre de pesquisa, exibir todos da saudação importado grupos ou todos os computadores que pertencem a tooeach grupo. Usando a [Pesquisa de Log](log-analytics-log-searches.md), você pode iniciar uma análise detalhada de dados do Configuration Manager.

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisa de Log](log-analytics-log-searches.md) tooview informações detalhadas sobre os dados do Configuration Manager.
