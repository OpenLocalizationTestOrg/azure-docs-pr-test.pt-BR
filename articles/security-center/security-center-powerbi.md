---
title: "informações de aaaGet dos dados da Central de segurança do Azure com o Power BI | Microsoft Docs"
description: "Olá pacote de conteúdo do Power BI do Centro de segurança do Azure torna fácil toofind alertas de segurança, recomendações, atacado recursos e mostra as tendências, com base em um conjunto de dados que foi criado para o seu relatório."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Obtenha percepções de dados da Central de Segurança do Azure com o Power BI
Olá [painel do Power BI](http://aka.ms/azure-security-center-power-bi) para a Central de segurança do Azure permite que você toovisualize, analisar e filtrar as recomendações e alertas de segurança de qualquer lugar, incluindo o seu dispositivo móvel. Use as tendências do hello Power BI painel tooreveal e ataques padrões - exibir alertas de segurança por recurso ou endereço IP de origem e periféricos riscos de segurança por recurso ou idade.

Você também pode combinar recomendações e alertas de segurança do Security Center com outros dados de maneiras interessantes, por exemplo, usando dados dos [Logs de auditoria do Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) e da [Auditoria do Banco de Dados SQL do Azure](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Oferecem painéis do Power BI, e você também pode exportar esse tooExcel de dados para relatórios fácil no estado de segurança de saudação de seus recursos de nuvem.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Usando a Central de segurança do Azure painel tooaccess Power BI
Você também pode usar relatórios do Power BI Olá Central de segurança do Azure painel tooaccess. Execute Olá etapas tooperform essa tarefa:

1. Em Olá **Central de segurança do Azure** painel, clique em **Power BI** botão.

    ![Conecte-se a Central de segurança tooAzure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Olá **Power BI** folha abre Olá direita, como mostrado na Olá tela a seguir:

    ![Conecte-se a Central de segurança tooAzure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Se você estiver criando o painel do Power BI Olá para Olá primeira vez, você pode escolher Olá seguinte opções no hello **explorar no Power BI** folha:

   * **Painel de informações de segurança**: Escolha esta opção se você quiser que um painel que inclui o status de segurança, threads e detecções de toocreate. Esta opção é a mais comum para a função DevOps responsável pela análise de seu status de proteção e alertas detectados nas assinaturas.
   * **Painel de gerenciamento de política**: Escolha esta opção se você quiser tooexplore gerenciamento e imposição de política.  Esta opção é a mais comum para a TI Central, que está mais focada na governança. Eles podem usar essa visibilidade do painel toogain e ideias na conformidade de política de segurança em toda a empresa.
   * Se você já tiver um painel do Power BI, clique em **painel do Power BI atual Go tooyour**.
4. Neste exemplo, clique na opção **Painel de informações de segurança** . Se isso for Olá pela primeira vez, você está criando um painel do Power BI para a Central de segurança tiver solicitado tooinstall pacote de conteúdo de saudação. Clique em **obter** botão Olá **pacotes de conteúdo para o Power BI** janela conforme mostrado no hello tela a seguir:

    ![Painel de Informações de Segurança da Central de Segurança do Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Olá **conectar tooAzure Security Center segurança Insights** janela exibida. Verifique se Olá **autenticação** método é **oAuth2** conforme mostrado abaixo e clique em **entrar** botão.

    ![Autenticação](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Talvez você seja solicitado tooauthenticate novamente com suas credenciais do Azure. Depois de autenticar, seu painel será criado. Depois de criar o painel de saudação você ver um relatório com uma estrutura semelhante hello, conforme mostrado no hello tela a seguir:

    ![Painel do Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Uma atualização de relatório Olá é local tootake agendado diariamente. Se houver uma falha nessa atualização, leia [possíveis problemas de atualização com hello Power BI do Centro de segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), para obter mais informações sobre como tootroubleshoot.
>
>

Aqui você pode ver o número de saudação de alertas de segurança e as recomendações, bem como número de saudação de VMs, bancos de dados SQL do Azure e os recursos de rede que está sendo monitorados pelo Centro de segurança do Azure.

Um link de tooAzure Central de segurança redireciona toohello portal do Azure. gráficos de saudação torná-lo fácil toovisualize informações sobre recomendações de segurança e alertas, incluindo:

* Estado da Segurança de Recursos
* Recomendações Pendentes
* Recomendações de VM
* Alertas ao Longo do Tempo
* Recursos Atacados
* IPs Atacados

Por trás de cada gráfico, há percepções adicionais. Selecione um bloco toosee obter mais informações. Por exemplo, Olá **estado de segurança do recurso** bloco mostra detalhes adicionais sobre pendentes recomendações pelos recursos conforme Olá tela a seguir:

![Recomendações](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Se você clicar em qualquer linha do gráfico, hello outras pessoas estão acontecendo toogray out e você se concentre somente Olá selecionado por você. tooreturn toohello painel, clique em **Central de segurança do Azure** em Olá **painéis** opção no painel esquerdo do hello desta página.

> [!NOTE]
> Se você gostaria que toocustomize seus relatórios, adicionando campos adicionais ou alterar elementos visuais existentes, você poderá editar o relatório de saudação. Leia [Interagir com um relatório no Modo de Edição no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) para saber mais.
>
>

Olá **alertas ao longo do tempo, recursos de atacado** e **invasor IPs** blocos terão saída semelhante hello quando você clica em cada um dele. Isso acontece porque o relatório de saudação agrega as informações sobre esses três variáveis e chamá-lo **recursos sob ataque** conforme Olá tela a seguir:

![Recursos sob Ataque](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

Agora você pode também salvar uma cópia deste relatório, imprimi-lo ou publicá-lo na web hello usando Olá opções disponíveis no hello **arquivo** menu.

![Menu Arquivo](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Como explorar seus dados da Central de Segurança do Azure com serviços do Power BI
Conecte-se toohello [serviços de pacote de conteúdo do Power BI](https://msit.powerbi.com/groups/me/getdata/services) no Power BI e executar Olá etapas a seguir:

1. Em Olá **pacote de conteúdo para o Power BI** janela, você verá duas opções, conforme mostrado abaixo.

    ![Pacote de Conteúdo do Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Se já executada a primeira parte Olá deste artigo, você verá somente uma opção, que é o gerenciamento de política de Central de segurança do Azure.
   >
   >
2. Para fins de saudação deste exemplo, clique em **obter** em Olá **gerenciamento de política de Central de segurança do Azure** lado a lado.
3. Em Olá **conectar tooAzure gerenciamento de política de segurança Center** janela, tooselect se tornar **oAuth2** em **método de autenticação** drop para baixo, conforme mostrado abaixo e clique em **Entrar** botão.

    ![Janela de Gerenciamento de Política](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Você será redirecionado tooan página de autenticação onde você deve digitar as credenciais de saudação que você está usando a Central de segurança tooAzure tooconnect. Após a conclusão do processo de autenticação hello, Power BI será iniciar a importação de dados toobuild seus relatórios. Durante esse tempo, talvez você veja Olá a seguinte mensagem no canto direito de saudação do navegador:

    ![Conecte-se a Central de segurança tooAzure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Quando o painel hello está sendo criado para Olá primeira vez pode levar mais tempo, principalmente para cenários em que você tiver várias assinaturas.
   >
   >
5. Depois que o processo de saudação é concluído, o painel do Power BI do Centro de segurança do Azure será carregado com hello **gerenciamento de política** relatório semelhante toohello mostrado abaixo:

    ![Painel de gerenciamento da política](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como toouse Power BI na Central de segurança do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Planejamento da Central de segurança do Azure e guia de operações](security-center-planning-and-operations-guide.md) — Saiba como tooplan adoção da Central de segurança do Azure.
* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure as configurações de segurança na Central de segurança do Azure
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure
