---
title: "aaaMicrosoft Dynamics CRM e informações de aplicativo do Azure | Microsoft Docs"
description: "Obtenha a telemetria do Microsoft Dynamics CRM Online usando o Application Insights. Passo a passo da instalação, obtenção de dados, visualização e exportação."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Passo a passo: Ativar a telemetria para o Microsoft Dynamics CRM Online usando o Application Insights
Este artigo mostra como os dados de telemetria tooget do [Microsoft Dynamics CRM Online](https://www.dynamics.com/) usando [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Vamos examinar o processo completo de saudação de adicionar Application Insights script tooyour aplicativo, a captura de dados e visualização de dados.

> [!NOTE]
> [Procurar a solução de exemplo hello](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Adicionar Application Insights toonew ou instância do CRM Online
toomonitor seu aplicativo, você adiciona um aplicativo de tooyour do SDK do Application Insights. Olá SDK envia telemetria toohello [portal do Application Insights](https://portal.azure.com), onde você pode usar nossa análise avançada e ferramentas de diagnóstico ou exportar Olá toostorage de dados.

### <a name="create-an-application-insights-resource-in-azure"></a>Criar um recurso do Application Insights no Azure
1. Obtenha [uma conta no Microsoft Azure](http://azure.com/pricing). 
2. O logon no hello [portal do Azure](https://portal.azure.com) e adicionar um novo recurso do Application Insights. Este é o local em que os dados serão processados e exibidos.
   
    ![Clique em +, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Escolha o ASP.NET como o tipo de aplicativo hello.
3. Abra a página de introdução de saudação e "Monitor e o diagnóstico do lado do cliente".
   
    ![Trecho de código para inserção na sua página da Web](./media/app-insights-sample-mscrm/03.png)

**Manter a página de código Olá aberta** enquanto Olá próxima etapa em outra janela do navegador. Você precisará código Olá em breve. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Criar um recurso da Web em JavaScript no Microsoft Dynamics CRM
1. Abra sua instância do CRM Online e faça logon com privilégios de administrador.
2. Abra o Microsoft Dynamics CRM configurações, as personalizações, personalizar Olá sistema
   
    ![Configurações do Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Configurações > Personalizações](./media/app-insights-sample-mscrm/05.png)

    ![Personalizar a opção de saudação do sistema](./media/app-insights-sample-mscrm/06.png)

1. Crie um recurso de JavaScript.
   
    ![Caixa de diálogo Novo Recurso da Web](./media/app-insights-sample-mscrm/07.png)
   
    Dê a ele um nome, selecione **Script (JScript)** e Olá abrir editor de texto.
   
    ![Editor de texto de saudação aberto](./media/app-insights-sample-mscrm/08.png)
2. Copie o código de saudação do Application Insights. Ao copiar Verifique tooignore certeza de marcas de script. Consulte a captura de tela abaixo:
   
    ![Configurar sua chave de instrumentação](./media/app-insights-sample-mscrm/09.png)
   
    código de saudação inclui a chave de instrumentação Olá que identifica o recurso do Application insights.
3. Salve e publique.
   
    ![Salvar e publicar](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Formulários de instrumento
1. No Microsoft CRM Online, abra o formulário de conta de saudação
   
    ![Formulário da Conta](./media/app-insights-sample-mscrm/11.png)
2. Abrir o formulário de saudação propriedades
   
    ![Propriedades do formulário](./media/app-insights-sample-mscrm/12.png)
3. Adicionar Olá recurso da web de JavaScript que você criou
   
    ![Adicionar menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Adicionar recurso da web de saudação](./media/app-insights-sample-mscrm/14.png)
4. Salve e publique as personalizações do formulário.

## <a name="metrics-captured"></a>Métricas capturadas
Você já configurou a captura de telemetria para o formulário de saudação. Sempre que for usado, dados serão enviados recurso do Application Insights tooyour.

Aqui estão exemplos de dados de saudação que você verá.

#### <a name="application-health"></a>Integridade do aplicativo
![Tempo de carregamento de página de exemplo](./media/app-insights-sample-mscrm/15.png)

![Gráfico de exibições de página de exemplo](./media/app-insights-sample-mscrm/16.png)

Exceções de navegador:

![Gráfico de exceções de navegador](./media/app-insights-sample-mscrm/17.png)

Clique em Olá gráfico tooget mais detalhes:

![Lista de exceções](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Uso
![Usuários, seções e exibição de página](./media/app-insights-sample-mscrm/19.png)

![Gráficos de sessão](./media/app-insights-sample-mscrm/20.png)

![Versões do navegador](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Navegadores
![Divisão de tempo de carregamento de página](./media/app-insights-sample-mscrm/22.png)

![Contagem de sessões por versão do navegador](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Geolocalização
![Contagem de sessões por país](./media/app-insights-sample-mscrm/24.png)

![Sessões e usuários por país](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Solicitação de exibição de página interna
![Resumo de exibição de página](./media/app-insights-sample-mscrm/26.png)

![Pesquisar em eventos de exibição de página](./media/app-insights-sample-mscrm/27.png)

![Exibições de páginas semelhantes](./media/app-insights-sample-mscrm/28.png)

![Propriedades de exibição de página](./media/app-insights-sample-mscrm/29.png)

![Páginas por sessão](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Exemplo de código
[Procurar o código de exemplo hello](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Você pode fazer uma análise mais profunda mesmo se você [exportar Olá dados tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Exemplo de Solução para o Microsoft Dynamics CRM
[Aqui está a solução de exemplo hello implementada no Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Saiba mais
* [O que é o Application Insights?](app-insights-overview.md)
* [Application Insights para páginas da Web](app-insights-javascript.md)
* [Mais exemplos e explicações passo a passo](app-insights-code-samples.md)
