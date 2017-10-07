---
title: "Padrão de aplicativo Web de locatário aaaMulti | Microsoft Docs"
description: "Localize visões gerais de arquitetura e padrões de design que descrevem como tooimplement um multilocatário web aplicativo no Azure."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Aplicativos multilocatários no Azure
Um aplicativo multilocatário é um recurso compartilhado que permite que o aplicativo de saudação de tooview separado de usuários ou "locatários," como se fosse seu próprio. Um cenário típico que presta aplicativo multilocatário tooa é aquele em que todos os usuários de saudação aplicativo pode desejar a experiência do usuário Olá toocustomize mas detêm Olá os mesmos requisitos de negócios básico. Exemplos de grandes aplicativos multilocatários são o Office 365, o Outlook.com e o visualstudio.com.

Da perspectiva de um provedor aplicativo, os benefícios de Olá de multilocação principalmente se relacionam toooperational e eficiência de custos. Uma versão do seu aplicativo pode atender às necessidades de saudação de locatários muitos/clientes, permitindo a consolidação do sistema de tarefas de administração, como monitoramento, ajuste de desempenho, manutenção de software e backups de dados.

a seguir Olá fornece uma lista de metas mais significativas do hello e os requisitos da perspectiva do provedor.

* **Provisionamento**: você deve ser capaz de tooprovision novos locatários para o aplicativo hello.  Para aplicativos multilocatários com um grande número de locatários, é geralmente necessário tooautomate esse processo, permitindo o provisionamento de autoatendimento.
* **Facilidade de manutenção**: você deve ser capaz de tooupgrade Olá aplicativo e executar outras tarefas de manutenção enquanto estiver usando vários locatários-lo.
* **Monitoramento**: você deve ser toomonitor capaz de aplicativo de hello em todos os momentos tooidentify quaisquer problemas e tootroubleshoot-los. Isso inclui monitoramento como cada locatário está usando o aplicativo hello.

Um aplicativo multilocatário implementado adequadamente fornece a seguinte Olá benefícios toousers.

* **Isolamento**: atividades Olá de locatários individuais não afeta o uso de saudação do aplicativo hello por outros locatários. Os locatários não podem acessar os dados uns dos outros. Parece toohello locatário que tiverem o uso exclusivo do aplicativo hello.
* **Disponibilidade**: locatários individuais deseja Olá aplicativo toobe constantemente disponível, talvez com garantias definidas em um SLA. Novamente, atividades de saudação de outros locatários não devem afetar a disponibilidade de saudação do aplicativo hello.
* **Escalabilidade**: aplicativo hello dimensiona toomeet demanda de saudação de locatários individuais. Olá presença e ações de outros locatários não devem afetar desempenho de saudação do aplicativo hello.
* **Os custos**: custos são menores que a execução de um aplicativo dedicado, único locatário, porque permite a multilocação Olá compartilhamento de recursos.
* **Capacidade de personalização**. Olá capacidade toocustomize Olá aplicativo para um locatário individual de várias maneiras, como adicionar ou remover recursos, alterar os logotipos e cores ou até mesmo adicionar seu próprio código ou script.

Resumindo, embora haja várias considerações que você deve levar em conta tooprovide um serviço altamente escalonável, também há um número de metas de saudação e requisitos de aplicativos de vários locatários toomany comuns. Alguns podem não ser relevantes em cenários específicos e a importância de saudação individuais metas e requisitos serão diferentes em cada cenário. Como um provedor de aplicativo multilocatário hello, você também terá metas e requisitos, como reunião locatários Olá metas e requisitos, lucratividade, cobrança, vários níveis de serviço, provisionamento, monitoramento de facilidade de manutenção e automação.

Para obter mais informações sobre considerações de design adicionais de um aplicativo multilocatário, consulte [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure] (Hospedando um aplicativo multilocatário no Azure). Para obter informações sobre os padrões comuns da arquitetura de dados dos aplicativos do banco de dados SaaS (software como serviço) multilocatário, consulte [Padrões de Design para Aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

O Azure fornece muitos recursos que permitem a você tooaddress Olá chave problemas encontrados durante a criação de um sistema multilocatário.

**Isolamento**

* Segmentar locatários de sites por Cabeçalhos de Host com ou sem comunicação SSL
* Segmentar locatários de site por parâmetros de consulta
* Serviços web em funções de trabalho
  * Funções de trabalho. que normalmente processa os dados em Olá back-end de um aplicativo.
  * Funções da Web que normalmente agem como Olá front-end para aplicativos.

**Armazenamento**

Gerenciamento de dados, como serviços de banco de dados do SQL Azure ou armazenamento do Azure como Olá tabela serviço que fornece serviços de armazenamento de grandes quantidades de dados não estruturados e Olá serviço Blob que fornece serviços toostore grandes quantidades de texto não estruturado ou dados binários, como imagens, áudio e vídeo.

* Proteção de logons no SQL Server por locatário apropriados para dados de multilocatários em Bancos de Dados SQL.
* Usando tabelas do Azure para o aplicativo de recursos, especificando uma política de acesso no nível do contêiner, você pode Olá permissões de tooadjust capacidade sem ter que tooissue nova URL para recursos de saudação protegidos com assinaturas de acesso compartilhado.
* As filas do Azure para filas do Azure de recursos do aplicativo são usada toodrive processamento em nome de locatários, mas também pode ser usado toodistribute trabalho necessário para provisionamento ou gerenciamento.
* Um serviço compartilhado de filas do barramento de serviço para recursos de aplicativos que tooa de trabalho de envios por push, você pode usar uma única fila onde cada remetente do locatário tem somente permissões (conforme derivado de declarações emitidas do ACS) toopush toothat fila ao somente receptores de saudação do serviço Olá ter permissão toopull dos dados de saudação de fila Olá provenientes de vários locatários.

**Serviços de conexão e segurança**

* Barramento de serviço do Azure, uma infraestrutura de mensagens que fica entre aplicativos, permitindo que eles tooexchange mensagens de uma maneira flexível para maior escala e resiliência.

**Serviços de rede**

O Azure fornece vários serviços de rede que oferecem suporte à autenticação e melhoram a capacidade de gerenciamento dos aplicativos hospedados. Esses serviços incluem o seguinte hello:

* A Rede Virtual do Azure permite que você provisione e gerencie VPNs (redes virtuais privadas) no Azure e vincule-as com segurança à infraestrutura de TI local.
* Gerenciador de tráfego de rede virtual permite balancear tooload tráfego de entrada entre vários hospedados do Azure services se estiver em execução no hello mesmo datacenter ou em data centers diferentes em torno de Olá, mundo.
* O Active Directory do Azure (AD do Azure) é um serviço moderno e baseado em REST que fornece recursos de gerenciamento de identidade e de controle de acesso para seus aplicativos na nuvem. Usando o AD do Azure para recursos do aplicativo do Azure AD tooprovides uma maneira fácil de autenticar e autorizar usuários toogain acesso tooyour aplicativos e serviços web ao permitir que os recursos de saudação de autenticação e autorização toobe fatorados fora do seu código.
* O Service Bus do Azure fornece um serviço de mensagens seguro e o recurso de fluxo de dados para aplicativos distribuídos e híbridos, como a comunicação entre aplicativos hospedados do Azure e aplicativos e serviços locais, sem a necessidade de firewall complexo e de infraestruturas de segurança. Usando a retransmissão de barramento de serviço para toohello de recursos do aplicativo de serviços que são expostos como pontos de extremidade podem pertencer toohello locatário (por exemplo, hospedado fora do sistema hello, como no local), ou eles podem ser serviços provisionados especificamente para Olá locatário ( porque os dados confidenciais, específico do locatário trafegam entre eles).

**Provisionando recursos**

Azure fornece várias maneiras de novos locatários de provisionamento para o aplicativo hello. Para aplicativos multilocatários com um grande número de locatários, é geralmente necessário tooautomate esse processo, permitindo o provisionamento de autoatendimento.

* Funções de trabalho permitem tooprovision e provisionamento de recursos por locatário (por exemplo, quando um novo locatário se cadastra ou cancela), coletar métricas para medição de uso e o gerenciamento de escala seguindo certa programação ou na interseção de toohello de resposta de limites de chave indicadores de desempenho. Essa mesma função também pode ser usado toopush solução de toohello de atualizações.
* Blobs do Azure podem ser usado tooprovision computação ou recursos de armazenamento já foi inicializado para novos locatários proporcionando contêiner acesso ao nível políticas tooprotect Olá computação pacotes de serviço, imagens VHD e outros recursos.
* As opções para provisionamento de recursos de Banco de Dados SQL para um locatário incluem:
  
  * DDL em scripts ou incorporada como recursos em assemblies
  * Pacotes de DAC do SQL Server 2008 R2 implantados programaticamente.
  * Cópia de um banco de dados mestre de referência
  * Usando o banco de dados de importação e exportação tooprovision novos bancos de dados de um arquivo.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
