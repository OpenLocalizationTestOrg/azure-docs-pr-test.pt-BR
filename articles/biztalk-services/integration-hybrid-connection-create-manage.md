---
title: "aaaCreate e gerenciar conexões híbridas | Microsoft Docs"
description: "Saiba como toocreate uma conexão híbrida, gerenciar conexão hello e instalar Olá Gerenciador de Conexão híbrida. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Criar e gerenciar Conexões Híbridas

> [!IMPORTANT]
> As Conexões Híbridas do BizTalk foram desativadas e substituídas pelas Conexões Híbridas do Serviço de Aplicativo. Para obter mais informações, incluindo como toomanage as conexões existentes de híbrida do BizTalk, consulte [conexões híbridas dos serviços de aplicativo do Azure](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Visão geral das etapas de saudação
1. Criar uma Conexão híbrida inserindo Olá **nome de host** ou **FQDN** do recurso de local de saudação em sua rede privada.
2. Vincule seus aplicativos web do Azure ou aplicativos móveis do Azure toohello Conexão híbrida.
3. Instalar Gerenciador de Conexão híbrida de saudação no recurso local e conectar toohello Conexão específica de híbrida. Olá portal do Azure fornece uma experiência de único clique tooinstall e conecte-se.
4. Gerenciar Conexões Híbridas e suas chaves de conexão.

Este tópico lista estas etapas. 

> [!IMPORTANT]
> É possível tooset um endereço IP de tooan de ponto de extremidade de Conexão híbrida. Se você usar um endereço IP, você pode ou não alcançar o recurso de local de hello, dependendo de seu cliente. Olá Conexão híbrida depende de cliente Olá fazendo uma pesquisa de DNS. Na maioria dos casos, Olá **cliente** é o código do aplicativo. Se hello cliente executa uma pesquisa DNS, (ele não tente tooresolve Olá endereço IP como se fosse um nome de domínio (x.x.x. x)), em seguida, o tráfego não é enviado por meio de saudação Conexão híbrida.
> 
> Por exemplo (pseudocódigo), você define **10.4.5.6** como seu host local:
> 
> **Olá funciona cenário a seguir:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **Olá cenário a seguir não funciona:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Criar uma Conexão Híbrida
Uma Conexão híbrida podem ser criado em Olá portal do Azure usando os aplicativos Web **ou** usando os serviços do BizTalk. 

**toocreate conexões híbridas com aplicativos Web**, consulte [tooan conectar os aplicativos Web do Azure recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md). Você também pode instalar Olá Gerenciador de Conexão híbrida (HCM) de seu aplicativo web, que é o método preferido de hello. 

**toocreate conexões híbridas nos Serviços BizTalk**:

1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação esquerdo hello, selecione **Serviços BizTalk** e, em seguida, selecione o BizTalk Service. 
   
    Se não tiver um Serviço BizTalk, você poderá [Criar um Serviço BizTalk](biztalk-provision-services.md).
3. Selecione Olá **conexões híbridas** guia:  
   ![Guia de Conexões Híbridas][HybridConnectionTab]
4. Selecione **criar uma Conexão híbrida** ou selecione hello **adicionar** botão na barra de tarefas de saudação. Digite hello seguinte:
   
   | Propriedade | Descrição |
   | --- | --- |
   | Nome |Olá Conexão híbrida nome deve ser exclusivo e não pode ser Olá mesmo nome como Olá BizTalk Service. Você pode inserir qualquer nome, mas seja específico quanto à sua finalidade. Alguns exemplos incluem: <br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Clientes*OracleServer* |
   | Nome de host |Insira nome de host totalmente qualificado do hello, somente nome de host do hello, ou Olá endereço IPv4 do recurso de local de saudação. Os exemplos incluem:<br/><br/>mySQLServer<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>Se você usar o endereço IPv4 de hello, observe que o código de cliente ou aplicativo não pode resolver o endereço IP de saudação. Consulte Olá importante observação na parte superior da saudação deste tópico. |
   | Porta |Insira o número da porta de saudação do recurso de local de saudação. Por exemplo, se você estiver usando Aplicativos Web, insira a porta 80 ou 443. Se você estiver usando o SQL Server, insira a porta 1433. |
5. Selecione Olá marca de seleção toocomplete Olá configuração. 

#### <a name="additional"></a>Adicional
* Conexões Híbridas adicionais podem ser criadas. Consulte Olá [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md) para número de saudação de conexões permitidas. 
* Cada Conexão Híbrida é criada com um par de cadeias de conexão: chaves de aplicativo que ENVIAM e chaves locais que ESCUTAM. Cada par possui uma chave primária e outra secundária. 

## <a name="LinkWebSite"></a>Vincular seu Aplicativo Móvel ou aplicativo Web ou do Serviço de Aplicativo do Azure
Selecione um aplicativo Web ou aplicativo móvel toolink no serviço de aplicativo do Azure tooan existente de Conexão híbrida, **usar uma Conexão híbrida existente** na folha de conexões híbridas hello. Confira [Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Instalar Olá o Gerenciador de Conexão híbrida local
Depois que uma Conexão híbrida é criada, instale Olá Gerenciador de Conexão híbrida no recurso de local de saudação. É possível fazer o download por meio dos aplicativos Web do Azure ou por meio de seu Serviço BizTalk. Etapas dos Serviços BizTalk: 

1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação esquerdo hello, selecione **Serviços BizTalk** e, em seguida, selecione o BizTalk Service. 
3. Selecione Olá **conexões híbridas** guia:  
   ![Guia de Conexões Híbridas][HybridConnectionTab]
4. Na barra de tarefas hello, selecione **configuração local**:  
   ![Configuração Local][HCOnPremSetup]
5. Selecione **instalar e configurar** toorun ou download Olá Gerenciador de Conexão híbrida na Olá sistema local. 
6. Selecione Olá marca de seleção toostart Olá instalação. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Adicional
* Gerenciador de Conexão híbrida pode ser instalado em Olá sistemas operacionais a seguir:
  
  * Windows Server 2008 R2 (.NET Framework 4.5+ e Windows Management Framework 4.0+ obrigatório)
  * Windows Server 2012 (Windows Management Framework 4.0+ obrigatório)
  * Windows Server 2012 R2
* Depois de instalar Olá Gerenciador de Conexão híbrida, ocorre a seguinte Olá: 
  
  * Olá Conexão híbrida hospedados no Azure é configurado automaticamente toouse Olá cadeia de Conexão de aplicativo principal. 
  * recurso de local de saudação é configurada automaticamente toouse Olá cadeia de caracteres de Conexão no local primário.
* Olá Gerenciador de Conexão híbrida deve usar uma cadeia de caracteres de conexão de local válido para autorização. Aplicativos de Web do Azure Hello ou aplicativos móveis deve usar uma cadeia de caracteres de conexão de aplicativo válido para autorização.
* Você pode dimensionar conexões híbridas instalando outra instância do Gerenciador de Conexão híbrida de saudação em outro servidor. Configure Olá local ouvinte toouse Olá mesmo endereço como o primeiro ouvinte de local hello. Nessa situação, o tráfego de saudação é distribuído aleatoriamente (round robin) entre ouvintes do hello local ativa. 

## <a name="ManageHybridConnection"></a>Gerenciar Conexões Híbridas
toomanage suas conexões híbridas, você pode:

* Use Olá portal do Azure e vá tooyour BizTalk Service. 
* Usar [APIs REST](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Copie/gere novamente cadeias de Conexão híbrida Olá
1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação esquerdo hello, selecione **Serviços BizTalk** e, em seguida, selecione o BizTalk Service. 
3. Selecione Olá **conexões híbridas** guia:  
   ![Guia de Conexões Híbridas][HybridConnectionTab]
4. Selecione Olá Conexão híbrida. Na barra de tarefas hello, selecione **gerenciar Conexão**:  
   ![Gerenciar opções][HCManageConnection]
   
    **Gerenciar Conexão** listas Olá cadeias de caracteres de conexão de aplicativo e no local. Você pode copiar Olá cadeias de caracteres de Conexão ou regenerar Olá que chave de acesso usada na cadeia de caracteres de conexão de saudação. 
   
    **Se você selecionar regenerar**, Olá chave de acesso compartilhado usada dentro de saudação cadeia de caracteres de Conexão é alterada. Olá a seguir:
   
   * No portal clássico do Azure do hello, selecione **sincronizar as chaves** em Olá aplicativo do Azure.
   * Execute novamente a saudação **configuração local**. Quando você executar novamente a saudação no local de instalação, Olá recurso local é automaticamente configurado cadeia de caracteres de conexão primária do toouse Olá atualizado.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Saudação de toocontrol de política de grupo use recursos usados por uma Conexão híbrida local
1. Baixar Olá [modelos administrativos do Gerenciador de Conexão híbrida](http://www.microsoft.com/download/details.aspx?id=42963).
2. Extraia os arquivos de saudação.
3. No computador de saudação que modifica a política de grupo, Olá a seguir:  
   
   * Saudação de cópia. Arquivos ADMX que toohello *%WINROOT%\PolicyDefinitions* pasta.
   * Saudação de cópia. ADML arquivos toohello *%WINROOT%\PolicyDefinitions\en-us* pasta.

Após a cópia, você pode usar a diretiva de saudação toochange do Editor de diretiva de grupo.

## <a name="next"></a>Avançar
[Conecte-se a aplicativos Web do Azure tooan recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Conecte-se o SQL Server local tooon de aplicativos Web do Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Visão geral de Conexões Híbridas](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Consulte também
[API REST para gerenciamento dos Serviços do BizTalk no Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md)  
[Criar um Serviço BizTalk usando o Portal de clássico do Azure](biztalk-provision-services.md)  
[Serviços BizTalk: guias Painel, Monitor e Escala](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
