---
title: "aaaWhat é o Azure Analysis Services | Microsoft Docs"
description: "Obter um panorama de saudação do Analysis Services no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>O que é o Azure Analysis Services?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services fornece na nuvem de saudação de modelagem de dados de nível empresarial. É uma plataforma totalmente gerenciada como um serviço (PaaS), integrada com os serviços de plataforma de dados do Azure. 

Com o Analysis Services, você pode realizar o mashup e combinar dados de várias fontes, definir métricas e proteger seus dados em um modelo de dados simples, semântico e confiável. modelo de dados de saudação fornece uma maneira rápida e fácil para seu usuários toobrowse grandes quantidades de dados com aplicativos cliente como o Power BI, Excel, Reporting Services, os aplicativos de terceiros e personalizados.

![Fontes de dados](./media/analysis-services-overview/aas-overview-data-sources.png)

Check-out [este vídeo](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn como Azure Analysis Services se encaixa em Microsoft geral do recursos de BI e como você pode se beneficiar de obter os modelos de dados em nuvem hello.

## <a name="built-on-sql-server-analysis-services"></a>Criado no SQL Server Analysis Services
O Azure Analysis Services é compatível com os mesmos recursos incríveis já presentes no SQL Server Analysis Services Enterprise Edition. Serviços de análise do Azure oferece suporte a modelos de tabela no hello 1200 e 1400 [níveis de compatibilidade](analysis-services-compat-level.md). Partições, segurança em nível de linha, relações bidirecionais e traduções: todos têm suporte. Os modos na memória e DirectQuery significam consultas muito rápidas em conjuntos de dados grandes e complexos.

Os modelos de tabela oferecem desenvolvimento rápido e são altamente personalizáveis. Para desenvolvedores, modelos de tabela incluem objetos de modelo de toodescribe de modelo de objeto de tabela (TOM) hello. TOM é exposto em JSON por meio de saudação [linguagem de script de modelo Tabular (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) e linguagem de definição de dados do AMO por meio de saudação do hello [AnalysisServices](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) namespace.

## <a name="better-with-azure"></a>Melhor com o Azure
Serviços de análise do Azure se integra com muitos serviços do Azure, permitindo que você toobuild sofisticado soluções de análise. Integração com [Active Directory do Azure](../active-directory/active-directory-whatis.md) fornece dados críticos de tooyour acesso seguro, baseado em função. Integrar [do Azure Data Factory](../data-factory/data-factory-introduction.md) pipelines, incluindo uma atividade que carrega dados no modelo de saudação. A [Automação do Azure](../automation/automation-intro.md) e o [Azure Functions](../azure-functions/functions-overview.md) podem ser usados para coordenação leve de modelos usando código personalizado.

## <a name="get-up-and-running-quickly"></a>Entre rapidamente em funcionamento
No Portal do Azure, você pode [criar um servidor](analysis-services-create-server.md) em questão de minutos. E, com [modelos](../azure-resource-manager/resource-manager-create-first-template.md) do Azure Resource Manager e o PowerShell, você pode provisionar servidores usando um modelo declarativo. Com um único modelo, você pode implantar vários serviços com outros componentes do Azure, como contas de armazenamento e o Azure Functions. 

Depois que você tiver um servidor criado, é possível criar um modelo de tabela diretamente no portal do Azure. Com novos hello (visualização) [recurso designer Web](analysis-services-create-model-portal.md), você pode se conectar tooan banco de dados do SQL Azure, fonte de dados do Azure SQL Data Warehouse, ou importar um arquivo do Power BI Desktop. pbix. As relações entre tabelas são criadas automaticamente, e você pode criar medidas ou editar o arquivo de model.bim de saudação no formato json à direita do seu navegador.

## <a name="scale-tooyour-needs"></a>Necessidades de tooyour de escala
O Azure Analysis Services está disponível nas camadas de Desenvolvedor, Básica e Standard. Em cada camada, os custos do plano variam de acordo tooprocessing power, QPUs e tamanho da memória. Quando você cria um servidor, é possível selecionar um plano de dentro de uma camada. Você pode alterar os planos de ou para baixo em Olá mesmo nível ou camada superior tooa atualização, mas você não pode fazer o downgrade de um nível mais baixo do mais alto nível tooa.

Escalar verticalmente, reduzir verticalmente ou pausar o servidor. Use Olá portal do Azure ou ter controle total sobre rapidamente usando o PowerShell. Você paga apenas pelo que usa. toolearn mais sobre Olá diferentes planos e camadas e use Olá preços Calculadora toodetermine Olá plano certo para você, consulte [preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Manter seus dados próximos a você
Servidores de serviços de análise do Azure podem ser criados no seguinte Olá [regiões do Azure](https://azure.microsoft.com/regions/):

| Américas | Europa | Pacífico Asiático |
|----------|--------|--------------|
|  Sul do Brasil<br> Canadá Central<br> Leste dos EUA 2<br> Centro-Norte dos EUA<br> Centro-Sul dos Estados Unidos<br> Centro-Oeste dos EUA<br> Oeste dos EUA | Norte da Europa<br> Sul do Reino Unido<br> Europa Ocidental |   Sudeste da Austrália<br> Leste do Japão<br> Sudeste Asiático<br> Índia Ocidental  |

Novas regiões estão sendo adicionados tempo Olá todo, para que essa lista pode estar incompleta. Escolha um local ao criar o servidor no portal do Azure ou usando modelos do Azure Resource Manager. Olá tooget melhor desempenho, escolha um local mais próximo de sua base de usuários maior. Garanta uma [alta disponibilidade](analysis-services-bcdr.md) ao implantar seus modelos em servidores redundantes em várias regiões.

## <a name="migrate-your-existing-tabular-models"></a>Migrar seus modelos de tabela existentes
Se você já tiver as soluções existentes de modelo do SQL Server Analysis Services local, você pode migrar tooAzure Analysis Services sem alterações significativas. toomigrate, você pode usar o SSDT toodeploy seu servidor de tooyour de modelo. Ou, no SSMS, você pode usar o backup e a restauração ou TMSL.

Se você tiver fontes de dados local, você precisa tooinstall e configurar um [gateway de dados no local](analysis-services-gateway.md). Se você tiver funções e membros da função já configurados, migrar suas funções, mas você tem membros da função tooreadd usando o SSMS ou o PowerShell.

## <a name="connect-toopopular-data-sources"></a>Conectar fontes de dados toopopular
Azure Analysis Services oferece suporte a [conectar fontes toodata](analysis-services-datasource.md) local em sua organização e na nuvem hello. Combine dados de fontes de dados locais e na nuvem para uma solução de híbrida. 

Novos modelos de tabela 1400 usam o recurso de obter dados moderno de saudação no SSDT, com base na linguagem de fórmula consulta Olá M. Com obter dados, você tem mais de transformação de dados e recursos de mashup e Olá capacidade toocreate e editar suas próprias consultas de linguagem de fórmula avançadas M. Por exemplo, com modelos de tabela 1400, você pode modelar arquivos de dados no Armazenamento de Blobs do Azure.

## <a name="use-hello-tools-you-already-know"></a>Usar as ferramentas de saudação que você já sabe

![Ferramentas de desenvolvedor BI](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) para Visual Studio
Desenvolver e implantar modelos com hello livre [SQL Server Data Tools (SSDT) para o Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). O SSDT inclui modelos de projeto do Analysis Services que o deixa pronto rapidamente. SSDT agora inclui Olá moderna obter dados fonte de dados de consulta e mashup funcionalidade 1400 para modelos de tabela. Se você estiver familiarizado com obter dados no Power BI Desktop e Excel 2016, você já sabe como é fácil toocreate altamente personalizada consultas de fonte de dados.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Gerencie seus servidores e bancos de dados modelo usando o [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Conecte servidores tooyour na nuvem hello. Executar scripts TMSL à direita da janela de consulta XMLA hello e automatizar tarefas usando scripts TMSL. Novos recursos e funcionalidades acontecem rapidamente. O SSMS é atualizado mensalmente.

#### <a name="powershell"></a>PowerShell
Tarefas de gerenciamento de recursos de servidor como criação de servidores, suspender ou retomar operações de servidor ou alterar o nível de serviço da saudação (camada) usam cmdlets do Gerenciador de recursos do Azure (AzureRM). Outras tarefas de gerenciamento de bancos de dados como adicionar ou remover membros da função, processar ou execução de scripts TMSL usar cmdlets no módulo do SqlServer hello. Módulos AzureRM e SQL Server estão disponíveis em Olá [Galeria do PowerShell](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Seus dados estão seguros
![Visualizações de dados](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Autenticação
A autenticação de usuário para o Azure Analysis Services é feita pelo [AAD (Azure Active Directory)](../active-directory/active-directory-whatis.md). Quando você tenta toolog no banco de dados do Azure Analysis Services tooan, use usuários uma identidade de conta da organização com o banco de dados do access toohello que elas pretendem tooaccess. Essas identidades de usuário devem ser membros do padrão de saudação do Active Directory do Azure para a assinatura de saudação onde hello Azure Analysis Services servidor reside. mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).

#### <a name="data-security"></a>Segurança de dados
Serviços de análise do Azure utiliza toopersist de armazenamento de BLOBs do Azure e os metadados para bancos de dados do Analysis Services. Os arquivos de dados no blob são criptografados usando Azure SSE (criptografia do servidor de blobs). Ao usar o modo Consulta Direta, apenas os metadados serão armazenados. os dados reais Olá são acessados Olá da fonte de dados no momento da consulta.

#### <a name="on-premises-data-sources"></a>Fontes de dados locais
Acesso seguro toodata residentes no local em sua organização é obtida instalando e configurando um [gateway de dados no local](analysis-services-gateway.md). Gateways fornecem acesso toodata para consulta direta e modos de memória. Quando um modelo do Azure Analysis Services se conecta a fonte de dados local tooan, uma consulta será criada juntamente com hello criptografado credenciais Olá local fonte de dados. serviço de nuvem do gateway Olá analisa a consulta hello e envia Olá solicitação tooan barramento de serviço do Azure. gateway de local de saudação sonda hello Azure Service Bus para solicitações pendentes. gateway Hello, em seguida, obtém Olá consulta, descriptografa Olá credenciais e conecta-se a fonte de dados de toohello para execução. Olá resultados são então enviados da fonte de dados de hello, fazer toohello gateway e, em seguida, em serviços de análise do Azure toohello banco de dados.

Serviços de análise do Azure é controlado por Olá [termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e hello [declaração de privacidade do Microsoft Online Services](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn mais sobre a segurança do Azure, consulte Olá [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Dá suporte a ferramentas de cliente mais recentes Olá
![Visualizações de dados](./media/analysis-services-overview/aas-overview-clients.png)

Ferramentas modernas de exploração de dados e visualização como o Power BI, Excel e ferramentas de terceiros fornecem aos usuários ideias altamente interativas e visualmente avançadas sobre seus dados de modelo.

Os clientes usam MSOLAP, AMO ou ADOMD [bibliotecas de cliente](analysis-services-data-providers.md) servidores de serviços de tooAnalysis tooconnect. Os aplicativos cliente da Microsoft, como o Power BI Desktop e o Excel, instalam as três bibliotecas de cliente. Mas tenha em mente, dependendo da versão de saudação ou a frequência de atualizações, bibliotecas de cliente podem não ser versões mais recentes de saudação exigidas pelo Azure Analysis Services. Olá mesmo se aplica toocustom aplicativos ou outras interfaces, como AsCmd, TOM, ADOMD.NET. Esses aplicativos normalmente exigem instalando bibliotecas Olá manualmente como parte de um pacote.


## <a name="get-help"></a>Obter ajuda

#### <a name="documentation"></a>Documentação
Serviços de análise do Azure é toomanage e tooset simple para cima. Você pode encontrar todas as informações de saudação necessário toocreate e gerenciar os serviços do servidor aqui. Ao criar um servidor de tooyour de toodeploy de modelo de dados, ele tem muito Olá mesmo assim como para criar um modelo de dados que você implantar o servidor de local de tooan. Existe uma ampla biblioteca de artigos conceituais, procedimentais, tutoriais e de referência em [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services).

#### <a name="videos"></a>Vídeos
Confira alguns vídeos úteis em [Azure Analysis Services no Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services).

#### <a name="blogs"></a>Blogs
As coisas estão mudando rapidamente. Você sempre pode obter informações mais recentes Olá Olá [blog da equipe do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) e [blog Azure](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Comunidade
O Analysis Services tem uma comunidade de usuários vibrante. Ingressar na conversa Olá em [Fórum do Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Comentários
Quer fazer sugestões ou solicitações de recursos? Ser tooleave-se de que seus comentários em [Azure Analysis Services comentários](https://aka.ms/azureanalysisservicesfeedback).

Tiver sugestões sobre a documentação de Olá? Você pode adicionar comentários usando Livefyre na parte inferior da saudação de cada artigo.

## <a name="next-steps"></a>Próximas etapas
Agora que você saiba mais sobre os serviços de análise do Azure, é hora tooget iniciado. Saiba como muito[criar um servidor](analysis-services-create-server.md) no Azure. Quando o servidor estiver pronto, percorrer Olá [tutorial do Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn como toocreate um modelo de tabela totalmente funcional e implantá-lo tooyour server.
