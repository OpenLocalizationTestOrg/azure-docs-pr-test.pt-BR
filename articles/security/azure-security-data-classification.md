---
title: "aaaData classificação para o Azure | Microsoft Docs"
description: "Este artigo fornece uma introdução toohello conceitos básicos da classificação de dados e realça a seu valor, especificamente no contexto de saudação da nuvem de computação e usando o Microsoft Azure"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Classificação de dados para o Azure
Este artigo fornece uma introdução toohello conceitos básicos da classificação de dados e realça a seu valor, especificamente no contexto de saudação da nuvem de computação e de uso do Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Conceitos básicos de classificação de dados
A classificação de dados bem-sucedida em uma organização exige amplo conhecimento das necessidades da organização e uma compreensão completa de onde residem seus ativos de dados.  

Os dados existem em um destes três estados básicos: 

* Em repouso 
* Em andamento 
* Em trânsito 

Todos os três estados exigem exclusivas soluções técnicas para classificação de dados, mas hello aplicados princípios da classificação de dados deve ser hello mesmo para cada um. Dados que são classificados como confidenciais precisam toostay confidenciais quando em repouso, no processo e em trânsito. 

Os dados também podem ser estruturados ou não estruturados. Processos de classificação típico para Olá estruturado dados encontrados em bancos de dados e planilhas são menos complexa e demorada toomanage que os dados não estruturados, como email, documentos e código-fonte. 

> [!TIP]
> para saber mais sobre recursos do Azure e práticas recomendadas para criptografia de dados, leia [Práticas recomendadas de criptografia de dados do Azure](azure-security-data-encryption-best-practices.md)
> 
> 

Em geral, as organizações têm mais dados não estruturados do que dados estruturados. Independentemente se os dados são estruturados ou não, é importante para você toomanage dados sensibilidade. Quando implementada corretamente, classificação de dados ajuda a garantir que os dados confidenciais ativos são gerenciados com maior supervisão de ativos de dados que são considerados toodistribute público ou livre. 

### <a name="controlling-access-toodata"></a>Controlando acesso toodata
Autenticação e autorização são frequentemente confundidos um com o outro e suas funções são mal compreendidas. Na realidade são bastante diferentes, conforme mostrado na figura a seguir de saudação.  

![Controle e acesso a dados](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Autenticação
Autenticação normalmente consiste em pelo menos duas partes: um tooidentify de ID de usuário ou nome de usuário um usuário e um token, como uma senha, tooconfirm que Olá credencial de nome de usuário é válido. processo de saudação não fornece Olá o usuário autenticado com acesso tooany itens ou serviços; ele verifica que o usuário Olá é quem diz.   

> [!TIP]
> [Active Directory do Azure](../active-directory/active-directory-whatis.md) fornece serviços de identidade baseados em nuvem que permitem que você tooauthenticate e autorizam usuários. 
> 
> 

### <a name="authorization"></a>Autorização
A autorização é o processo de saudação de fornecer um tooaccess de capacidade de saudação do usuário autenticado, um aplicativo, o conjunto de dados, o arquivo de dados ou algum outro objeto. Atribuir usuários autenticados Olá direitos toouse, modificar ou excluir os itens que eles possam acessar requer a classificação de toodata de atenção. 

Autorização bem-sucedida requer a implementação de um mecanismo toovalidate individuais dos usuários precisa tooaccess arquivos e informações com base em uma combinação de função, política de segurança e considerações sobre política de risco. Por exemplo, dados de aplicativos de (LOB) de linha de negócios específicos talvez não seja necessário toobe acessado por todos os funcionários, e somente um pequeno subconjunto de funcionários provavelmente precisará de acesso toohuman arquivos de RH (recursos). Mas, para as organizações toocontrol quem pode acessar dados, bem como quando e como, um sistema efetivo para autenticar os usuários deve estar em vigor. 

> [!TIP]
> no Microsoft Azure, verifique se tooleverage o Access RBAC (controle) toogrant somente Olá quantidade de acesso que os usuários precisam tooperform seus trabalhos. Leitura [usar recursos de Active Directory do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md) para obter mais informações. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Funções e responsabilidades na computação em nuvem
Embora os provedores de nuvem podem ajudar a gerenciar os riscos, os clientes precisam tooensure esse gerenciamento de classificação de dados e imposição é implementada corretamente tooprovide Olá nível apropriado de serviços de gerenciamento de dados.  

Classificação de dados responsabilidades irão variar com base em qual modelo de serviço de nuvem está em vigor, conforme mostrado na figura a seguir de saudação. três modelos de serviço de nuvem primária Olá são infraestrutura como serviço (IaaS), plataforma como serviço (PaaS) e software como serviço (SaaS). Implementação de mecanismos de classificação de dados também irão variar com base na dependência hello e expectativas de provedor de nuvem hello. 

![Funções](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Embora você é responsável para classificar seus dados, provedores de nuvem devem assumir compromissos escritos sobre como eles serão proteger e manter a privacidade Olá Olá de dados do cliente armazenados em sua nuvem.  

* **Provedores de IaaS** requisitos são limitados tooensuring que Olá ambiente virtual pode acomodar as funcionalidades de classificação de dados e requisitos de conformidade do cliente. Provedores de IaaS têm uma função menor na classificação de dados porque eles só precisarem de tooensure que os dados do cliente atende aos requisitos de conformidade. No entanto, os provedores ainda devem garantir que seus ambientes virtuais atendem aos requisitos de classificação de dados em adição toosecuring seus data centers.
* **Provedores de PaaS** responsabilidades podem ser misturadas, porque a plataforma de saudação poderia ser usada em uma abordagem em camadas de segurança de tooprovide para uma ferramenta de classificação. Provedores de PaaS podem ser responsáveis pela autenticação e possivelmente algumas regras de autorização e devem fornecer segurança e a camada de aplicativo tootheir do recursos de classificação de dados. Muito como provedores de IaaS, PaaS provedores necessário tooensure sua plataforma está em conformidade com quaisquer requisitos de classificação de dados relevantes.
* **Provedores de SaaS** frequentemente será considerado como parte de uma cadeia de autorização e será necessário tooensure que Olá dados armazenados no aplicativo de SaaS hello pode ser controlado por tipo de classificação. Aplicativos SaaS podem ser usados para aplicativos de LOB e por natureza necessário tooprovide Olá significa tooauthenticate e autorizar os dados que são usados e armazenados. 

## <a name="classification-process"></a>Processo de classificação
Muitas organizações que entender Olá precisa para classificação de dados e desejar tooimplement um desafio básico: onde toobegin?

Uma maneira simple e eficaz tooimplement a classificação de dados é toouse Olá plano, fazer, verificação, o ato de modelo de [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). a seguir Olá Figura gráficos tarefas Olá toosuccessfully necessário implementar a classificação de dados nesse modelo.  

1. **PLANEJAR**. Identificar os ativos de dados, um programa de classificação de dados custodiante toodeploy Olá e desenvolver perfis de proteção. 
2. **FAZER**. Depois que as políticas de classificação de dados são acordadas, implantar o programa hello e implementar tecnologias de imposição conforme necessário para dados confidenciais.  
3. **VERIFICAR**. Verifique e valide relatórios tooensure ferramentas hello e métodos que estão sendo usados são efetivamente endereçamento Olá políticas de classificação. 
4. **AGIR**. Examine o status de saudação do acesso a dados e examine arquivos e dados que exigem revisão usando uma reclassificação e alterações de tooadopt de metodologia de revisão e tooaddress novos riscos.  

![Planejar, Fazer, Verificar, Agir](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Selecione um modelo de terminologia que atenda às suas necessidades
Existem vários tipos de processos de classificação de dados, incluindo processos manuais, processos com base no local que classificam os dados com base no local de um usuário ou do sistema, processos baseados em aplicativo, como classificação de banco de dados específico e automatizada processos usados pelo diversas tecnologias, alguns dos quais são descritos na seção de "Proteção de dados confidenciais" hello neste artigo.  

Este artigo introduz dois modelos de terminologia generalizada com base em modelos bastante usados e respeitados pelo setor. Esses modelos de terminologia, que fornecem três níveis de sensibilidade de classificação, são mostrados no Olá a tabela a seguir.  

> [!NOTE]
> ao classificar um arquivo ou recurso que combina dados que normalmente seriam classificados em níveis diferentes, o nível mais alto de saudação de classificação presente devem estabelecer Olá classificação geral. Por exemplo, um arquivo que contém dados confidenciais e restritos deve ser classificado como restrito.  
> 
> 

| **Confidencialidade** | **Modelo de terminologia 1** | **Modelo de terminologia 2** |
| --- | --- | --- |
| Alto |Confidencial |Restrito |
| Média |Apenas para uso interno |Sigiloso |
| Baixo |Público |Irrestrito |

#### <a name="confidential-restricted"></a>Confidencial (restrito)
Informações que são classificadas como confidenciais ou restritos incluem dados que podem ser tooone catastrófica ou mais pessoas e/ou organizações se comprometido ou perdido. Essas informações com frequência são fornecidas em uma base de "necessidade tooknow" e podem incluir: 

* Dados pessoais, incluindo informações de identificação pessoal, como números de Previdência Social ou de identificação nacional, números de passaporte, números de cartão de crédito, números de carteira de motorista, registros médicos e números de ID de apólice de seguros de saúde.  
* Registros financeiros, incluindo números de contas financeiras, como números de verificação ou de contas de investimentos. 
* Material de negócios, como documentos ou dados que são exclusivos ou propriedade intelectual específica.  
* Dados legais, incluindo material potencialmente privilegiado de advogados. 
* Dados de autenticação, incluindo chaves de criptografia particular, pares de nome de usuário e senha ou outras sequências de identificação, como arquivos de chave biométrica particulares. 

Frequentemente, os dados classificados como confidenciais têm requisitos regulatórios e de conformidade para manipulação de dados. 

#### <a name="for-internal-use-only-sensitive"></a>Apenas para uso interno (sigiloso)
Informações que são classificadas com um nível de sigilo médio incluem arquivos e dados que não causariam um impacto grave para um indivíduo e/ou uma organização caso perdidos ou destruídos. Essas informações podem incluir: 

* Email, a maioria dos quais pode ser excluída ou distribuída sem provocar uma crise (excluindo as caixas de correio ou de email de pessoas que são identificadas na classificação confidencial Olá).  
* Documentos e arquivos que não têm dados confidenciais.

Em geral, essa classificação inclui tudo o que não é confidencial. Essa classificação pode incluir a maioria dos dados de negócios, pois a maioria dos arquivos que são gerenciados ou usadas no dia a dia pode ser classificada como sigilosa. Com exceção de saudação de dados que são publicados ou são confidencial, todos os dados dentro de uma organização podem ser classificados como confidenciais por padrão. 

#### <a name="public-unrestricted"></a>Público (irrestrito)
Informações que são classificadas como público incluem dados e arquivos que não são críticas toobusiness necessidades ou operações. Essa classificação também pode incluir dados deliberadamente foi lançada toohello público para seu uso, como anúncios de material ou pressione de marketing. Além disso, essa classificação pode incluir dados como mensagens de email de spam armazenadas por um serviço de email. 

### <a name="define-data-ownership"></a>Definir a propriedade dos dados
É importante tooestablish uma cadeia de custódia claro de propriedade para todos os ativos de dados. Olá tabela a seguir identifica as funções de propriedade de dados diferentes no trabalho de classificação de dados e seus respectivos direitos.  

| **Função** | **Criar** | **Modificar/excluir** | **Delegar** | **Ler** | **Arquivar/restaurar** |
| --- | --- | --- | --- | --- | --- |
| Proprietário |X |X |X |X |X |
| Custodiante | | |X | | |
| Administrador | | | | |X |
| Usuário\* | |X | |X | |

**Os usuários podem receber direitos adicionais, como editar e excluir, de um custodiante* 

> [!NOTE]
> esta tabela não fornece uma lista completa de funções e direitos, mas apenas uma amostra representativa. 
> 
> 

Olá **proprietário do ativo de dados** é criador original de saudação do dados hello, que podem delegar a propriedade e atribuir curador. Quando um arquivo é criado, o proprietário de saudação deve ser capaz de tooassign uma classificação, o que significa que eles têm um toounderstand de responsabilidade que precisa toobe classificado como confidencial com base nas políticas de sua organização. Todos os dados do proprietário do ativo de dados podem ser classificados automaticamente apenas para uso interno (sigilosos), a menos que ele seja responsável pela propriedade ou criação de tipos de dados confidenciais (restritos). Com frequência, função de saudação do proprietário será alterada após Olá dados são classificados. Por exemplo, proprietário Olá pode criar um banco de dados de informações confidenciais e liberar seu custódia de dados toohello direitos.  

> [!NOTE]
> os proprietários dos ativos de dados geralmente usam uma combinação de serviços, dispositivos e mídia, alguns dos quais são particulares e alguns dos quais pertencem toohello organização. Uma política organizacional clara pode ajudar a garantir que o uso de dispositivos, como laptops e dispositivos inteligentes, esteja de acordo com as diretrizes de classificação de dados.  
> 
> 

Olá **custódia de ativos de dados** é atribuído pelo proprietário do ativo hello (ou seus representantes) toomanage Olá ativo acordo tooagreements com o proprietário do ativo hello ou de acordo com os requisitos de política aplicável. Idealmente, a função de custódia de saudação pode ser implementada em um sistema automatizado. Custodiante um ativo garante que os controles de acesso necessários são fornecidos e é responsáveis por gerenciar e proteger ativos de delegado tootheir cuidado. responsabilidades de saudação de custódia de ativos de saudação podem incluir:  

* Proteger Olá ativo de acordo com a direção do proprietário do ativo hello ou conformidade com o proprietário do ativo Olá 
* Garantir que as políticas de classificação sejam cumpridas 
* Informar os proprietários dos ativos de quaisquer alterações tooagreed-em controles de e/ou alterações de toothose anterior de procedimentos de proteção entrar em vigor 
* Proprietário do ativo toohello relatórios sobre remoção tooor alterações Olá ativo do responsáveis 
* Um **administrador** representa um usuário que é responsável por garantir que a integridade seja mantida, mas ele não é um proprietário de ativos de dados, um custodiante nem um usuário. Na verdade, muitas funções de administrador fornecem serviços de gerenciamento de contêiner de dados sem a necessidade de acessar os dados toohello. a função de administrador Olá inclui backup e restauração dos dados hello, mantendo os registros de ativos de saudação e escolhendo, adquirir e operar Olá dispositivos e armazenamento que ativos de saudação de casa. 
* usuário do recurso Olá inclui qualquer pessoa que é concedido acesso toodata ou um arquivo. Atribuição de acesso geralmente é delegada por custódia de ativos de toohello Olá proprietário.  

### <a name="implementation"></a>Implementação
Considerações de gerenciamento se aplicam a tooall metodologias de classificação. Essas considerações necessário tooinclude detalhes sobre quem, o que, em que, quando e por que um ativo de dados deve ser usado, acessado, alterado ou excluído. Todo o gerenciamento ativo deve ser feito com uma compreensão de como uma organização exibe os riscos, mas pode ser aplicada uma metodologia simple, conforme definido no processo de classificação de dados de saudação. Considerações adicionais para a classificação de dados incluem a introdução de saudação de novos aplicativos e ferramentas e gerenciamento de alterações depois que um método de classificação for implementado.  

### <a name="reclassification"></a>Reclassificação
Reclassificação ou alteração do estado de classificação de saudação de um ativo de dados precisa toobe feito quando um usuário ou sistema determina a importância do ativo de dados que hello ou perfil de risco foi alterado. Esse trabalho é importante para garantir que o status de classificação Olá continua toobe atual e válido. A maior parte do conteúdo que não é classificado manualmente pode ser classificado automaticamente ou com base no uso por um custodiante de dados ou pelo proprietário dos dados. 

### <a name="manual-data-reclassification"></a>Reclassificação de dados manual
Idealmente, esse esforço garantiria que detalhes de saudação de uma alteração são capturados e auditados. a razão mais provável Olá para manual reclassificação seria por motivos de diferenciação, ou para registros mantidos em formato de documento ou uma necessidade tooreview de dados que foi originalmente classificadas incorretamente. Porque este documento considera toohello movimentação de dados na nuvem e classificação de dados, os esforços de reclassificação manual exigem atenção caso a caso e uma revisão de gerenciamento de riscos seria ideal tooaddress requisitos de classificação. Em geral, essa tentativa seria considere a política da organização Olá sobre o que precisa toobe classificado, Olá estado de classificação padrão (todos os dados e arquivos sendo confidenciais, mas não confidencial) e levar exceções para dados de alto risco. 

### <a name="automatic-data-reclassification"></a>Reclassificação de dados automática
Reclassificação de dados automática usa Olá mesmo geral de regra como classificação manual. exceção de saudação é que soluções automatizadas podem garantir que as regras são seguidas e aplicadas conforme necessário. A classificação de dados pode ser feita como parte de uma política de imposição de classificação de dados, que pode ser imposta quando dados são armazenados em uso e em trânsito usando a tecnologia de autorização.

* Baseada em aplicativo. O uso de determinados aplicativos por padrão define um nível de classificação. Por exemplo, dados de software de CRM (gerenciamento de relacionamento com o cliente), RH e ferramentas de gerenciamento de registro de saúde são confidenciais por padrão. 
* Baseada em local. O local dos dados pode ajudar a identificar a confidencialidade dos dados. Por exemplo, os dados armazenados por um HR ou o departamento financeiro são mais provável toobe confidencial por natureza.  

### <a name="data-retention-recovery-and-disposal"></a>Retenção, recuperação e descarte de dados
A recuperação e o descarte de dados, assim como a reclassificação de dados, são um aspecto essencial do gerenciamento de ativos de dados. Hello princípios para recuperação de dados e descarte seria definidos por uma política de retenção de dados e imposta Olá mesma maneira que reclassificação de dados; Essa tentativa será executada por Olá custódia e funções de administrador como uma tarefa de colaboração.  

Falha toohave uma política de retenção de dados pode significar toocomply de perda ou a falha de dados com os requisitos normativos e legais de descoberta. A maioria das organizações que não têm uma política de retenção de dados bem-definidos tendem toouse uma política de retenção padrão "manter tudo". No entanto, essa política de retenção tem riscos adicionais em cenários de serviços de nuvem. 

Por exemplo, uma política de retenção de dados para provedores de serviços de nuvem pode ser considerada como "hello durante saudação assinatura" (contanto que serviço Olá é pago para, Olá dados são retidos). Esse contrato de pagamento para retenção talvez não lide com políticas de retenção corporativas ou regulatórias. A definição de uma política para dados confidenciais pode garantir que os dados sejam armazenados e removidos com base nas práticas recomendadas. Além disso, uma diretiva de arquivamento pode ser criada tooformalize um entendimento sobre quais dados deve ser descartado de e quando. 

Política de retenção de dados deve ser abordados Olá necessário normativos e requisitos de conformidade, bem como requisitos corporativos retenção legal. Os dados confidenciais podem provocar questões quanto à duração da retenção e às exceções para dados que foram armazenados com um provedor. Essas questões são mais prováveis para dados que não foram classificados corretamente. 

> [!TIP]
> Saiba mais sobre as políticas de retenção de dados do Azure e muito mais lendo Olá [o contrato de assinatura do Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Proteção de dados confidenciais
Depois que os dados são classificados, localizando e implementar os dados confidenciais maneiras tooprotect se torna parte integrante de qualquer estratégia de implantação de proteção de dados. Proteção de dados confidenciais requer dados de toohow atenção adicional são armazenados e transmitidos em arquiteturas convencionais, bem como em nuvem hello. 

Esta seção fornece informações básicas sobre algumas tecnologias que podem automatizar os esforços de imposição toohelp proteger os dados foram classificados como confidenciais. 

Como Olá mostra a figura a seguir, essas tecnologias podem ser implantadas como soluções baseadas em nuvem ou local — ou em um modo híbrido, com algumas delas implantado no local e alguns na nuvem hello. (Algumas tecnologias, como criptografia e gerenciamento de direitos, também estendem toouser dispositivos).  

![Tecnologias](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Software de gerenciamento de direitos
Uma solução para impedir a perda de dados é o software de gerenciamento de direitos. Ao contrário das abordagens que tentam toointerrupt fluxo de saudação de informações em pontos de saída em uma organização, o software de gerenciamento de direitos funciona nos níveis de profundidade em tecnologias de armazenamento de dados. Os documentos são criptografados, e o controle sobre quem pode descriptografá-los usa controles de acesso que são definidos em uma solução de controle de autenticação, como um serviço de diretório.  

> [!TIP]
> Você pode usar o Azure Rights Management (Azure RMS) como Olá informações proteção solução tooprotect dados em cenários diferentes. Leia [O que é o Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) para saber mais sobre essa solução do Azure.
> 
> 

Alguns dos benefícios de saudação do software de gerenciamento de direitos: 

* Informações confidenciais protegidas. Os usuários podem proteger seus dados diretamente usando aplicativos habilitados para gerenciamento de direitos. Não são necessárias etapas adicionais. A criação de documentos, o envio de email e a publicação de dados oferecem uma experiência de proteção de dados consistente. 
* Proteção acompanha os dados de saudação. Os clientes permanecem no controle de quem tem acesso tootheir dados, seja em nuvem hello, infra-estrutura de TI, ou na área de trabalho do usuário hello. As organizações podem escolher tooencrypt seus dados e restringir o acesso de acordo com tootheir requisitos de negócios. 
* Políticas de proteção de informações padrão. Os administradores e usuários podem usar políticas padrão para muitos cenários comerciais comuns, como "Confidencial da Empresa – Somente Leitura" e "Não Encaminhar". Um rico conjunto de direitos de uso são suportadas como ler, copiar, imprimir, salvar, editar e encaminhar tooallow flexibilidade na definição de direitos de uso personalizados. 

> [!TIP]
> você pode proteger dados no Armazenamento do Azure usando a [Criptografia do Serviço de Armazenamento do Azure](../storage/storage-service-encryption.md) para Dados em Repouso. Você também pode usar [criptografia de disco do Azure](azure-security-disk-encryption.md) toohelp proteger os dados contidos em discos virtuais usados para máquinas virtuais do Azure.
> 
> 

### <a name="encryption-gateways"></a>Gateways de criptografia
Gateways de criptografia operam em seus próprios serviços de criptografia tooprovide camadas por todos os dados de acesso com base em toocloud de redirecionamento. Essa abordagem não deve ser confundida com a de uma VPN (rede virtual privada). Gateways de criptografia são criada tooprovide um transparente soluções baseadas em toocloud da camada.   

Gateways de criptografia podem fornecer um meio toomanage e proteger os dados que foi classificados como confidencial, criptografando os dados em trânsito hello, bem como dados em repouso.  

Gateways de criptografia são colocados no fluxo de dados de saudação entre dispositivos de usuário e serviços de criptografia/descriptografia tooprovide centros de dados de aplicativo. Essas soluções, como VPNs, são predominantemente locais. Eles são tooprovide projetado com controle sobre chaves de criptografia, que ajuda a reduzir o risco de saudação de colocar dados saudação e gerenciamento de chaves com um provedor de terceiros. Essas soluções são desenvolvidas, semelhante a criptografia, toowork fluido e transparente entre usuários e o serviço de saudação. 

> [!TIP]
> Você pode usar tooextend de rota expressa do Azure suas redes locais em nuvem da Microsoft hello sobre uma conexão privada dedicada. Leia [Visão geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md) para saber mais sobre essa funcionalidade. Outras opções para conectividade entre locais entre sua rede local e o [Azure é uma VPN site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Prevenção de perda de dados
Perda de dados (às vezes chamado tooas vazamento de dados) é uma consideração importante e prevenção de saudação externo de perda de dados por meio de insiders acidental e mal-intencionados é muito importante para muitas organizações.  

As tecnologias de DLP (prevenção de perda de dados) podem ajudar a garantir que soluções como serviços de email não transmitam dados que foram classificados como confidenciais. As organizações podem tirar proveito dos recursos DLP produtos existentes toohelp evitar perda de dados. Esses recursos usam políticas que podem ser facilmente criadas do zero ou usando um modelo fornecido pelo provedor de saudação do software.  

Tecnologias DLP podem executar uma análise detalhada do conteúdo por meio de correspondências de palavra-chave, correspondências de dicionário, avaliação de expressão regular e outros exames de conteúdo toodetect conteúdo que viole as políticas DLP organizacionais. Por exemplo, DLP pode ajudar a evitar a perda de saudação do hello seguintes tipos de dados: 

* Números de Previdência Social e de identificação nacional 
* Informações bancárias 
* Números de cartão de crédito  
* Endereços IP 

Algumas tecnologias DLP também fornecem a configuração de DLP Olá capacidade toooverride hello (por exemplo, se uma organização precisa de processador de folha de pagamento tootransmit número do seguro Social informações tooa). Além disso, é possível tooconfigure DLP para que os usuários são notificados antes de tentar mesmo toosend informações confidenciais que não devem ser transmitidas. 

> [!TIP]
> Você pode usar o Office 365 DLP recursos tooprotect seus documentos. Leia [Controles de conformidade do Office 365: prevenção contra perda de dados](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) para saber mais.
> 
> 

## <a name="see-also"></a>Consulte também
* [Melhores práticas de Criptografia de Dados do Azure](azure-security-data-encryption-best-practices.md)
* [Práticas recomendadas de Gerenciamento de Identidade do Azure e segurança de controle de acesso](azure-security-identity-management-best-practices.md)
* [Blog da equipe de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

