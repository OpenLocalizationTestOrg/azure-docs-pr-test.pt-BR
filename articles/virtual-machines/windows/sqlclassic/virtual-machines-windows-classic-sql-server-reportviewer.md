---
title: aaaUse ReportViewer em um Site da Web | Microsoft Docs
description: "Este tópico descreve como toobuild um site do Microsoft Azure com o controle ReportViewer do Visual Studio de saudação que exibe um relatório armazenado em uma máquina Virtual Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Usar o ReportViewer em um site da Web hospedado no Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Você pode criar um site do Microsoft Azure com hello controle ReportViewer do Visual Studio que exibe um relatório armazenado em uma máquina Virtual Microsoft Azure. Olá controle ReportViewer está em um aplicativo Web que você cria usando Olá modelo do aplicativo Web do ASP.NET.

> [!IMPORTANT]
> modelos de aplicativo Web ASP.NET MVC Olá não dão suporte a controle do ReportViewer hello.

tooincorporate ReportViewer para o site do Microsoft Azure, você precisa de saudação toocomplete tarefas a seguir.

* **Adicionar** Assemblies toohello pacote de implantação
* **Configurar** Autenticação e Autorização
* **Publicar** Olá tooAzure de aplicativo da Web do ASP.NET

## <a name="prerequisites"></a>Pré-requisitos
Revise Olá a seção "recomendações gerais e práticas recomendadas" em [SQL Server Business Intelligence em máquinas virtuais Azure](../classic/ps-sql-bi.md).

> [!NOTE]
> Os controles ReportViewer são fornecidos com o Visual Studio Standard Edition ou versões posteriores. Se você estiver usando Olá Web Developer Express Edition, você deve instalar Olá [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) recursos de tempo de execução do ReportViewer toouse hello.
> 
> Não há suporte para o ReportViewer configurado em modo de processamento local no Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Adicionando Assemblies toohello pacote de implantação
Quando você hospeda os ASP.NET aplicativos locais, assemblies do ReportViewer Olá são geralmente instalados diretamente no cache de assembly global (GAC) Olá saudação do servidor do IIS durante a instalação do Visual Studio e podem ser acessados diretamente pelo aplicativo hello. No entanto, quando você hospeda o aplicativo ASP.NET na nuvem hello, Microsoft Azure não permite que qualquer coisa toobe instalado em Olá GAC, portanto você deve verificar se assemblies do ReportViewer Olá estão disponíveis localmente para seu aplicativo. Você pode fazer isso adicionando referências toothem em seu projeto e configurá-los toobe copiado localmente.

No modo de processamento remoto, Olá controle ReportViewer usa Olá assemblies a seguir:

* **Microsoft.ReportViewer.WebForms.dll**: contém o código do ReportViewer hello, que é necessário toouse ReportViewer em sua página. Uma referência para esse assembly é adicionada tooyour projeto quando você solta um controle ReportViewer em uma página ASP.NET em seu projeto.
* **Microsoft.ReportViewer.Common.dll**: contém classes usadas pelo Olá controle ReportViewer em tempo de execução. Ele não é adicionado automaticamente tooyour projeto.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd tooMicrosoft.ReportViewer.Common uma referência
* Clique com botão direito do seu projeto **referências** nó e selecione **adicionar referência**, selecionar assembly Olá Olá .NET guia e clique em **Okey**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>assemblies de saudação toomake localmente acessíveis pelo seu aplicativo ASP.NET
1. Em Olá **referências** pasta, clique em assembly de Microsoft.ReportViewer.Common Olá para que suas propriedades aparecem no painel de propriedades de saudação.
2. No painel de propriedades hello, defina **Copy Local** tooTrue.
3. Repita as etapas 1 e 2 para Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget pacote de idiomas do ReportViewer
1. Instale Olá apropriado Microsoft Report Viewer 2012 Runtime pacote redistribuível do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Idioma Olá selecione da lista suspensa de saudação e página de saudação obtém toohello redirecionado correspondente página do Centro de download.
3. Clique em **baixar** toostart download de saudação do ReportViewerLP.exe.
4. Depois de fazer o download do ReportViewerLP.exe, clique em **executar** tooinstall imediatamente, ou clique em **salvar** toosave-tooyour computador. Se você clicar em **salvar**, lembre-se de nome de saudação da pasta de saudação onde salvar o arquivo hello.
5. Localize a pasta de saudação onde você salvou o arquivo hello. Clique com o botão direito do mouse em ReportViewerLP.exe, clique em **Executar como administrador** e em **Sim**.
6. Depois de executar ReportViewerLP.exe, você verá Olá c:\WINDOWS\Assembly. possui arquivos de recurso de saudação **Microsoft.ReportViewer.Webforms.Resources** e **Microsoft** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure para controle do ReportViewer localizada
1. Baixe e instale o pacote redistribuível do Microsoft Report Viewer 2012 Runtime Olá pelo seguinte Olá acima instruções especificadas.
2. Criar <language> pasta Olá Olá de projeto e copie associada a arquivos de assembly de recurso existe. Olá toobe de arquivos de assembly de recurso copiado são: **Microsoft.ReportViewer.Webforms.Resources.dll** e **Microsoft.ReportViewer.Common.Resources.dll**. Selecione os arquivos de assembly de recurso hello e no painel de propriedades hello, defina **copiar tooOutput diretório** muito "**copiar sempre**".
3. Definir Olá Culture & UICulture para o projeto da web de saudação. Para obter mais informações sobre como tooset Olá cultura e cultura da interface do usuário para uma página da Web do ASP.NET, consulte [como: definir hello Culture e UI Culture para globalização de página da Web do ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Configurando a autenticação e a autorização
Olá ReportViewer precisa toouse credenciais apropriadas tooauthenticate com o servidor de relatório hello e Olá credenciais devem ser autorizadas por Olá tooaccess Olá relatórios do servidor desejado. Para obter informações sobre autenticação, consulte Olá white paper [relatório do Reporting Services controle do visualizador e servidores de relatório de máquina virtual com base do Microsoft Azure](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Publicar Olá tooAzure de aplicativo da Web do ASP.NET
Para obter instruções sobre como publicar um tooAzure de aplicativo Web ASP.NET, consulte [como: migrar e publicar tooAzure um aplicativo Web do Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) e [Introdução aos aplicativos Web e ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Se Olá comando Adicionar projeto de implantação do Azure ou Adicionar projeto de serviço de nuvem do Azure não aparecer no menu de atalho Olá no Gerenciador de soluções, você pode precisar do framework de destino do toochange Olá para Olá projeto too.NET Framework 4.
> 
> comandos de saudação dois fornecem basicamente Olá a mesma funcionalidade. Um ou Olá outro comando aparecerá no menu de atalho Olá dependendo da versão do hello SDK do Microsoft Azure que você instalou.
> 
> 

## <a name="resources"></a>Recursos
[Relatórios da Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[Business Intelligence do SQL Server em Máquinas Virtuais do Azure](../classic/ps-sql-bi.md)

[Use o PowerShell tooCreate um Azure VM com um modo de servidor de relatório nativo](../classic/ps-sql-report.md)

