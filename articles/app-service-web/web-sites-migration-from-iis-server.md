---
title: "aaaMigrate um tooAzure de aplicativo web do enterprise do serviço de aplicativo"
description: "Mostra como tooquickly Assistente de migração de aplicativos Web toouse migrar tooAzure de sites da Web IIS existente aplicativos de Web do serviço de aplicativo"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Migrar um tooAzure de aplicativo web do enterprise do serviço de aplicativo
Você pode facilmente migrar seus sites existentes que são executados no Internet Information Service (IIS) 6 ou posterior muito[aplicativos de Web do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> O Windows Server 2003 chegou ao fim do suporte em 14 de julho de 2015. Se você estiver hospedando os sites em um servidor IIS que é o Windows Server 2003, os aplicativos Web é uma maneira de baixo risco, baixo custo e baixo fricção tookeep seus sites online e Assistente de migração de aplicativos da Web podem ajudar a automatizar o processo de migração de saudação para você. 
> 
> 

[Assistente de migração de aplicativos de Web](https://www.movemetothecloud.net/) pode analisar a instalação do servidor IIS, identifique quais sites podem ser migrado tooApp serviço, realçar os elementos que não podem ser migrados ou não têm suporte na plataforma hello e, em seguida, migrar seus sites e tooAzure de bancos de dados associados.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementos verificados durante a análise de compatibilidade
Olá, o Assistente de migração cria um tooidentify de relatório de prontidão possíveis causas preocupação ou problemas de bloqueio que podem impedir uma migração bem-sucedida de local IIS tooAzure aplicativos de Web do serviço de aplicativo. Alguns Olá principais itens toobe atento são:

* Associações de porta – aplicativos Web somente dão suporte à porta 80 para HTTP e à porta 443 para tráfego HTTPS. Configurações de porta diferente serão ignoradas e o tráfego será roteado too80 ou 443. 
* Autenticação – os aplicativos Web dão suporte à Autenticação Anônima por padrão e à Autenticação de Formulários onde especificado por um aplicativo. A autenticação do Windows pode ser usada somente com a integração com o Active Directory do Azure e o ADFS. Não há suporte no momento para nenhuma outra forma de autenticação - por exemplo, Autenticação Básica. 
* Cache de Assembly Global (GAC) – Olá GAC não tem suporte em aplicativos da Web. Se seu aplicativo faz referência a assemblies que você normalmente implanta toohello GAC, você precisará pasta bin do toodeploy toohello aplicativo em aplicativos da Web. 
* Modo de compatibilidade IIS5 – não há suporte para esse modo nos aplicativos Web. 
* Pools de aplicativos – em aplicativos da Web, cada site e seus aplicativos filho executados no hello mesmo pool de aplicativos. Se o site tiver vários aplicativos filho utilizando vários pools de aplicativos, consolidá-los tooa único pool de aplicativos com as mesmas configurações ou migrar cada aplicativo do aplicativo tooa web separado.
* Componentes COM – os aplicativos Web não permitir o registro de saudação de componentes COM na plataforma de saudação. Se seus sites ou aplicativos fazer uso de todos os componentes COM, você deve reescrevê-los no código gerenciado e implantá-las com hello site ou aplicativo.
* Extensões ISAPI – aplicativos da Web pode dar suporte a uso de saudação de extensões ISAPI. Você precisa toodo Olá seguinte:
  
  * implantar Olá DLLs com seu aplicativo web 
  * registrar DLLs hello usando [Web. config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Coloque um arquivo de applicationHost.xdt na raiz do site Olá com conteúdo Olá descrito em "Permitir toobe de extensões ISAPI arbitrart carregados" [deste artigo](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Para obter mais exemplos de como toouse transformações de documentos XML com o seu site, consulte [transformar seu Site do Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Outros componentes, como SharePoint, extensões de servidor do FrontPage (FPSE), FTP, certificados SSL não serão migrados.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Como toouse Olá Assistente de migração de aplicativos Web
Esta seção percorre um exemplo tootoomigrate alguns sites que usam um banco de dados do SQL Server e em execução em uma máquina local, Windows Server 2003 R2 (IIS 6.0):

1. No hello IIS servidor ou computador cliente Navegue muito[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Instalar o Assistente de migração de aplicativos da Web, basta clicar em hello **servidor dedicado do IIS** botão. Mais opções de será opções Olá futuro próximo. 
3. Clique em Olá **instalar ferramenta** botão tooinstall Assistente de migração de aplicativos da Web em seu computador.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Você também pode clicar em **Download para instalar offline** toodownload um ZIP do arquivo de instalação em servidores não conectado toohello internet. Ou, você pode clicar em **carregar um relatório de preparação de migração existente**, que é toowork uma opção avançada com um migração preparação relatório existente que você gerou anteriormente (explicado posteriormente).
   > 
   > 
4. Em Olá **de instalação do aplicativo** tela, clique em **instalar** tooinstall em seu computador. Ele também instalará dependências correspondentes, como a implantação da Web, DacFX e IIS, se necessário. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Uma vez instalado, o Assistente de migração de aplicativos Web inicia automaticamente.
5. Escolha **migrar sites e bancos de dados de um servidor remoto tooAzure**. Insira as credenciais administrativas de saudação para o servidor remoto hello e clique em **continuar**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Obviamente, você pode escolher toomigrate do servidor de local de saudação. opção remote Olá é útil quando você deseja toomigrate sites de um servidor do IIS de produção.
   
   Neste momento a ferramenta de migração de saudação inspecionará Olá a configuração do servidor do IIS, como Sites, aplicativos, Pools de aplicativos e dependências tooidentify sites de candidato para a migração. 
6. saudação de captura de tela abaixo mostra os três sites – **Default Web Site**, **TimeTracker**, e **CommerceNet4**. Todos eles têm um banco de dados associado que desejamos toomigrate. Selecione todos os sites de saudação deseja tooassess e, em seguida, clique em **próximo**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Clique em **carregar** relatório de preparação de saudação tooupload. Se você clicar em **salvar o arquivo localmente**, você pode executar a ferramenta de migração de saudação novamente mais tarde e carregamento Olá salvou o relatório de preparação conforme observado anteriormente.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Depois que você carregar o relatório de preparação de saudação, o Azure executa análise de preparação e mostra Olá resultados. Ler os detalhes da avaliação de saudação para cada site e certifique-se de que você entende ou ter resolvido todos os problemas antes de continuar. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Clique em **começar a migração** toostart migração de saudação. Agora, você será redirecionado tooAzure toolog em sua conta. É importante que você faça logon com uma conta que tenha uma assinatura ativa do Azure. Se não tiver uma conta do Azure, é possível se inscrever para obter uma avaliação gratuita [aqui](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Selecionar conta de locatário hello, assinatura do Azure e toouse de região para seus aplicativos web do Azure migrados e bancos de dados e, em seguida, clique em **Iniciar migração**. Você pode selecionar Olá sites toomigrate mais tarde.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Na próxima tela de saudação você pode fazer alterações toohello configurações de migração padrão, como:
    
    * usar um banco de dados SQL Azure existente ou criar um novo banco de dados SQL do Azure e configurar suas credenciais
    * Selecione Olá sites toomigrate
    * definir nomes para aplicativos da web do Azure de saudação e seus bancos de dados SQL vinculados
    * Personalizar as configurações globais do hello e configurações no nível do site
    
    saudação de captura de tela abaixo mostra todos os sites de saudação selecionados para migração com as configurações padrão de saudação.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Olá **ativar o Azure Active Directory** caixa de seleção em configurações personalizadas integra Olá aplicativo de web do Azure com [Active Directory do Azure](../active-directory/active-directory-whatis.md) (Olá **diretório padrão**). Para obter mais informações sobre a sincronização do Azure Active Directory com o Active Directory local, consulte [Integração de diretórios](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Depois de fazer todas as alterações de saudação desejada, clique em **criar** toostart processo de migração de saudação. ferramenta de migração de saudação criar aplicativo web e banco de dados SQL do Azure e o Azure hello e, em seguida, publicar bancos de dados e conteúdo do site hello. andamento da migração Olá é claramente mostrado na ferramenta de migração de saudação e você verá uma tela de resumo no final de hello, os sites de saudação detalhes migrados, se elas foram bem-sucedidas, links toohello recém-criado do Azure aplicativos da web. 
    
    Se nenhum erro ocorre durante a migração, Olá será da ferramenta de migração claramente indica Olá falha e reversão Olá as alterações. Também será capaz de toosend relatório de erros de hello diretamente a equipe de engenharia toohello clicando Olá **enviar relatório de erros** botão, a pilha de chamadas Olá falha capturada e criar o corpo da mensagem. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Se migrar terá êxito sem erros, você também pode clicar Olá **fornecer Feedback** botão tooprovide quaisquer comentários diretamente. 
12. Clique em aplicativos web do Azure do hello links toohello e verificar que a migração de saudação foi bem-sucedida.
13. Agora você pode gerenciar Olá migrados aplicativos web no serviço de aplicativo do Azure. toodo isso, faça logon no hello [Portal do Azure](https://portal.azure.com).
14. No Portal do Azure do hello, abra toosee de folha de aplicativos Web hello seus sites migrados (mostrados como os aplicativos web) e clique em qualquer um deles toostart Olá web app, como configurar contínuo de publicação, criação de backups, o dimensionamento automático e monitorar o uso de gerenciamento ou desempenho.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

