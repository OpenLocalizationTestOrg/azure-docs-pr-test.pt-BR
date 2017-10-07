---
title: "aaaSecure um aplicativo no serviço de aplicativo do Azure"
description: "Saiba como toosecure um aplicativo web, o back-end do aplicativo móvel ou o aplicativo de API no serviço de aplicativo do Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Proteger um aplicativo no Serviço de Aplicativo do Azure
Este artigo ajuda você a começar a proteger seu aplicativo Web, o back-end do aplicativo móvel ou o aplicativo de API no Serviço de Aplicativo do Azure. 

A segurança no Serviço de Aplicativo do Azure tem dois níveis: 

* **Plataforma e infraestrutura de segurança** -confiança hello Azure toohave serviços que você precisa de coisas tooactually executar com segurança na nuvem de saudação.
* **Segurança do aplicativo** -você precisa toodesign Olá aplicativo em si com segurança. Isso inclui como você integrar com o Active Directory do Azure, como gerenciar certificados e como você certifique-se de que você pode conversar com segurança toodifferent serviços. 

#### <a name="infrastructure-and-platform-security"></a>Segurança de plataforma e infraestrutura
Porque o serviço de aplicativo mantém Olá VMs do Azure, armazenamento, conexões de rede, estruturas da web, gerenciamento e recursos de integração e muito mais, está ativamente protegida e protegido e passa por conformidade rígida e verifica se em uma base contínua toomake Isso:

* Os aplicativos do serviço de aplicativo são isolados de ambos os Olá Internet e de Olá recursos do Azure de outros clientes.
* A comunicação de segredos (por exemplo, cadeias de conexão) entre o aplicativo do Serviço de Aplicativo e outros recursos do Azure (por exemplo, Banco de Dados SQL) em um grupo de recursos permaneça dentro do Azure e não cruze nenhum limite de rede. Os segredos sejam sempre criptografados.
* Toda a comunicação entre seu aplicativo do Serviço de Aplicativo e recursos externos, como gerenciamento do PowerShell, interface de linha de comando, SDKs do Azure, APIs REST e conexões híbridas, seja corretamente criptografada.
* O gerenciamento de ameaças 24 horas por dia proteja recursos do Serviço de Aplicativo contra malware, DDoS (negação de serviços distribuído), MITM (man-in-the-middle) e outras ameaças. 

Para saber mais sobre segurança de plataforma e infraestrutura no Azure, confira [Centro de Confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Segurança de aplicativo
Enquanto o Azure é responsável por proteger infraestrutura hello e que seu aplicativo é executado na plataforma, é sua responsabilidade toosecure seu próprio aplicativo. Em outras palavras, você precisa toodevelop, implantar e gerenciar o código do aplicativo e o conteúdo de forma segura. Sem isso, o código do aplicativo ou o conteúdo ainda pode ser vulnerável toothreats como:

* Injeção de SQL
* Sequestro de sessão
* Script entre sites
* MITM no nível de aplicativo
* DDoS no nível de aplicativo

Uma discussão completa sobre considerações de segurança para aplicativos baseados na web está além do escopo deste documento hello. Como ponto de partida para obter mais orientações sobre como proteger seu aplicativo, consulte Olá [Web aplicativo segurança projeto (OWASP) abra](https://www.owasp.org/index.php/Main_Page), especificamente Olá [10 principais do projeto.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), que listas Olá 10 principais atual web críticos aplicativo falhas de segurança, conforme determinado pela membros OWASP.

## <a name="perform-penetration-testing-on-your-app"></a>Executar testes de penetração no aplicativo
Uma saudação mais fácil maneiras tooget iniciada com testes para vulnerabilidades em seu aplicativo de serviço de aplicativo é Olá toouse [integração com Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform um clique vulnerabilidade verificação em seu aplicativo. Você pode exibir resultados de teste de saudação em um relatório de fácil de entender e aprender como toofix cada vulnerabilidade com instruções passo a passo.

Se você preferir tooperform seu próprios penetração testes ou deseja toouse outro conjunto de scanner ou provedor, você deve seguir Olá [processo de aprovação de teste de penetração do Azure](https://security-forms.azure.com/penetration-testing/terms) e obter penetração de saudação desejada tooperform aprovação prévia testes.

## <a name="https"></a> Comunicação segura com os clientes
Se você usar o hello  **\*. azurewebsites.net** nome do domínio criado para seu aplicativo de serviço de aplicativo, você poderá usar imediatamente o HTTPS, pois um certificado SSL é fornecido para todos os  **\*. azurewebsites.net** nomes de domínio. Se seu site usa um [nome de domínio personalizado](app-service-web-tutorial-custom-domain.md), você pode carregar um certificado SSL muito[habilitar HTTPS](app-service-web-tutorial-custom-ssl.md) para o domínio personalizado hello.

Habilitando [HTTPS](https://en.wikipedia.org/wiki/HTTPS) pode ajudar a proteger contra ataques a MITM na comunicação de saudação entre seu aplicativo e seus usuários.

## <a name="secure-data-tier"></a>Camada de dados segura
Serviço de aplicativo altamente integra-se ao banco de dados SQL, que todas as cadeias de caracteres de conexão de saudação são criptografadas em todos os segmentos de saudação e são descriptografadas apenas em Olá VM que o aplicativo hello é executado no *e* apenas hello quando o aplicativo será executado. Além disso, o banco de dados do SQL Azure inclui muitos toohelp de recursos de segurança é proteger os dados do aplicativo de ameaças, incluindo [criptografia em repouso](https://msdn.microsoft.com/library/dn948096.aspx), [sempre criptografado](https://msdn.microsoft.com/library/mt163865.aspx), [ Mascaramento de dados dinâmicos](../sql-database/sql-database-dynamic-data-masking-get-started.md), e [detecção de ameaças](../sql-database/sql-database-threat-detection.md). Se você tiver dados confidenciais ou requisitos de conformidade, consulte [proteger seu banco de dados SQL](../sql-database/sql-database-security-overview.md) para obter mais informações sobre como toosecure seus dados.

Se você usar um provedor de banco de dados de terceiros, como ClearDB, consulte a documentação do provedor Olá diretamente em práticas recomendadas de segurança.  

## <a name="develop"></a> Desenvolvimento e implantação seguros
### <a name="publishing-profiles-and-publish-settings"></a>Publicando configurações de publicação de perfis e publicação
Ao desenvolver aplicativos, executando tarefas de gerenciamento, ou automatizar tarefas usando utilitários como **Visual Studio**, **Web Matrix**, **Azure PowerShell** ou hello **Azure Interface de linha de comando (CLI do Azure)**, você pode usar um *configurações de publicação* arquivo ou um *perfil de publicação*. Ambos os tipos de arquivo autenticação-lo com o Azure e devem ser protegidos tooprevent não autorizado acesso.

* Um arquivo de **configurações de publicação** contém
  
  * ID da assinatura do Azure
  * Um certificado de gerenciamento que permite que você tooperform tarefas de gerenciamento para sua assinatura *sem ter que tooprovide um nome de conta ou senha*.
* Um arquivo de **perfil de publicação** contém
  
  * Informações de publicação de aplicativo tooyour

Se você usar um utilitário que usa um arquivo de configurações de publicação ou o arquivo de perfil de publicação, importar arquivo hello que contém as configurações de publicação de saudação ou perfil no utilitário Olá e, em seguida, **excluir** arquivo hello. Se for necessário manter arquivo hello, tooshare com outras pessoas trabalhando em projeto de hello, por exemplo, armazená-lo em um local seguro, como um *criptografado* diretório com permissões restritas.

Além disso, assegure-se de credenciais de saudação importada são protegidas. Por exemplo, **Azure PowerShell** e hello **Azure Interface de linha de comando (CLI do Azure)** ambos armazenam informações importadas no seu **diretório base** ( *~*  em sistemas Linux ou OS X e */usuários/seu nome de usuário* em sistemas Windows.) Para obter segurança adicional, você poderá muito**criptografar** esses locais usando as ferramentas de criptografia disponíveis para seu sistema operacional.

### <a name="configuration-settings-and-connection-strings"></a>Definições de configuração e cadeias de conexão
É comum cadeias de conexão de toostore prática, as credenciais de autenticação e outras informações confidenciais em arquivos de configuração. Infelizmente, esses cookies podem ser expostos no site ou pode haver check-in deles em um repositório público, expondo essas informações. Uma pesquisa simples em [GitHub](https://github.com), por exemplo, pode revelar inúmeros arquivos de configuração com segredos expostos em repositórios públicos hello.

Olá prática recomendada é tookeep essas informações fora de arquivos de configuração do aplicativo. Serviço de aplicativo permite que você armazene informações de configuração como parte do ambiente de tempo de execução Olá **configurações do aplicativo** e **cadeias de caracteres de conexão**. valores de saudação são expostos tooyour aplicativo em tempo de execução por meio de *variáveis de ambiente* para a maioria das linguagens de programação. Para aplicativos do .NET, esses valores são injetados na configuração do .NET durante o tempo de execução. Além dessas situações, esses parâmetros de configuração permanecerão criptografados, a menos que você exiba ou configure-as usando Olá [Portal do Azure](https://portal.azure.com) ou utilitários como o PowerShell ou hello CLI do Azure. 

Armazenar informações de configuração no serviço de aplicativo possibilita toolock do administrador do aplicativo hello informações confidenciais para aplicativos de produção de hello. Os desenvolvedores podem usar um conjunto separado de definições de configuração para desenvolvimento de aplicativos e configurações de saudação podem ser substituídas automaticamente pelas configurações de saudação configuradas no serviço de aplicativo. Os desenvolvedores de saudação nem mesmo precisam segredos de saudação tooknow configurados para o aplicativo de produção de hello. Para obter mais informações sobre como configurar definições de aplicativo e cadeias de conexão no Serviço de Aplicativo, confira [Configurando aplicativos Web](web-sites-configure.md).

### <a name="ftps"></a>Protocolo FTPS
Serviço de aplicativo do Azure fornece seguro sistema de arquivos FTP access toohello para seu aplicativo por meio de **FTPS**. Isso permite o código do aplicativo hello toosecurely acesso no aplicativo web de hello, bem como diagnóstico logs. É recomendável usar sempre FTPS em vez de FTP. 

link FTPS Olá para seu aplicativo pode ser encontrada com hello etapas a seguir:

1. Olá abrir [Portal do Azure](https://portal.azure.com).
2. Selecione **Procurar Tudo**.
3. De saudação **procurar** folha, selecione **serviços de aplicativos**.
4. De saudação **serviços de aplicativos** folha, o aplicativo desejado Olá Select.
5. Na folha de saudação do aplicativo, selecione **todas as configurações**.
6. De saudação **configurações** folha, selecione **propriedades**.
7. Olá FTP e FTPS são fornecidos links em Olá **configurações** folha. 

Para obter mais informações sobre o protocolo FTPS, consulte [Protocolo FTPS](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre segurança Olá Olá plataforma Windows Azure, informações sobre o relatório de um **incidente de segurança ou abuso**, ou tooinform Microsoft que você execute **teste de penetração** do seu site, consulte a seção de segurança de saudação do hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Para saber mais sobre os arquivos **web.config** ou **applicationhost.config** em aplicativos do Serviço de Aplicativo, confira [Configuration options unlocked in Azure App Service web apps](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/) (Opções de configuração desbloqueadas em aplicativos Web do Serviço de Aplicativo do Azure).

Para saber mais sobre como registrar em log informações de aplicativos do Serviço de Aplicativo, que podem ser úteis na detecção de ataques, confira [Habilitar o registro em log de diagnóstico](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo de início de curta duração no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

