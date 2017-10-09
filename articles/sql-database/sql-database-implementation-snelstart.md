---
title: aaaAzure estudo de caso do Azure do banco de dados SQL - Snelstart | Microsoft Docs
description: "Saiba mais sobre como toorapidly de banco de dados SQL usa SnelStart expandido seus serviços de negócios a uma taxa de 1.000 novo Azure bancos de dados SQL por mês"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Com o Azure, a SnelStart expandiu rapidamente seus serviços comerciais a uma taxa de 1.000 novos Bancos de Dados SQL do Azure por mês
![Logotipo da SnelStart](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart torna os Olá Holanda popular financeiros e business-software de gerenciamento para pequenas e médias empresas (SMB). Seus 55.000 clientes são atendidos por uma equipe de 110 funcionários, incluindo uma equipe de TI de 35 pessoas. Movendo de oferta de software-como um serviço (SaaS) tooa de software de área de trabalho criada no Azure, SnelStart feitas hello mais de serviços internos, automatizar o gerenciamento usando o ambiente familiar em c# e otimizar o desempenho e escalabilidade por nenhum failover ou provisionamento empresas usando pools elásticos. Usando o Azure fornece SnelStart fluidez de saudação da movimentação de clientes entre locais e hello nuvem.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Por que SnelStart estendidos serviços da nuvem de área de trabalho toohello Olá
> "Trabalhando com o Azure significa que podemos fornecer software mais rápido, rapidamente reagir toocustomer demandas e dimensionar soluções quando aumenta a demanda."
> 
> — Henry Been, arquiteto de software
> 
> 

A SnelStart comandou uma empresa de software bem-sucedida durante anos usando um modelo tradicional de desenvolvimento: código, pacote, envio e repetição. Ao longo do tempo, Olá ritmo de alteração cresceu mais rápido e mais rápido. Normas alterados com frequência, e clientes necessário mais fácil maneiras tooprocess registros e colaboram com seus contadores e governo tookeep backup com essas alterações.

"Envio toocustomers de software foi cara e limitação," de acordo com o tooHenry foi, arquiteto de software. "Os custos de produção, embalagem e envio limitavam a frequência de lançamento de software. Tivemos toopackage atualizações para remessas periódicas, mas que fez toomeet rígido alteração necessidades de nossos clientes. Podemos pode nunca ter certeza de que nossos clientes atualizados toohello a versão mais recente do produto hello. Portanto, tivemos que toosupport várias versões, tornando Olá suporte toodo muito difícil trabalho bem."

Foi adiciona, "queríamos uma maneira atualizações tooprogram e versão em acelerada impor um ritmo, portanto, poderia inovar mais rápido e criar novos serviços para nossos clientes. Também queremos que tooautomate uma maneira mais processos em ordem toosimplify necessidades de administração de negócios de nossos clientes."

Para SnelStart, Olá solução foi tooextend seus serviços, tornando-se um provedor de SaaS com base em nuvem. plataforma de banco de dados do Azure SQL Olá ajudou SnelStart chegar lá sem incorrer em Olá principais sobrecarga de TI que exigiria uma solução de infraestrutura-como-um-serviço (IaaS).

o modelo de nuvem Olá também permite SnelStart toofix bugs e fornece novos recursos rapidamente, sem que os clientes que precisam de atualização de software e toodownload. Acordo tooBeen, "serviços de nuvem do Azure usando nos permite usar tooquickly alterações de requisitos de terceiros. Em vez de ter tooship um toothousands versão nova de clientes, podemos pode adaptar informações enviadas do nosso formatos de toonew de aplicativo de área de trabalho necessários por terceiros."

## <a name="a-modern-company-with-traditional-roots"></a>Uma empresa moderna com raízes tradicionais
SnelStart é uma empresa moderna, agile, alta tecnologia com raízes humilde desde too1964, quando fundadores Olá iniciado empresa hello como um fabricante de partes de instrumentos musicais. núcleo de saudação do hello SnelStart comercial de software realmente iniciado superando em Olá década de 1980, durante a proliferação de saudação do PC hello. empresa de saudação necessário um software de contabilidade de toohello alternativa melhor disponível em tempo de saudação levou assuntos em suas próprias mãos. 1982, empresa Olá criado foundation saudação do que eventualmente se tornarão SnelStart software de contabilidade. A partir do início do hello, software de saudação foi admirada por sua simplicidade e velocidade — tanto que empresa Olá eventualmente alterado foco e reinventada em si em uma empresa de software.

Em 1995, a SnelStart lançou seu primeiro aplicativo de contadoria para Windows. aplicativo Hello, criado no banco de dados do Microsoft Visual Basic 1.0 e o Microsoft Access ajudou a crescer Olá toomore base do cliente de 5.000 usuários.

Hoje, a SnelStart é um dos principais provedores de um aplicativo de administração de negócios e LOB (linha de negócios) destinado às SMBs e aos empreendedores autônomos da Holanda. Como Carlo Kuip, arquiteto de TI, diz "nosso objetivo é tooprovide 100 por cento automação de serviços de administração de negócios para nossos clientes."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Otimizando desempenho e custo com pools elásticos
A SnelStart foi uma pioneira de grande escala na adoção dos pools elásticos. Pools Elásticos ajudam os custos de limite do hello da empresa e gerenciar os requisitos de desempenho com mais eficiência. De acordo com o tooBeen, "usando pools Elásticos, é possível otimizar o desempenho com base nas necessidades de saudação de nossos clientes, sem o excesso de provisionamento. Se tivéssemos tooprovision com base na carga de pico, seria muito cara. Olá em vez disso, os recursos de tooshare opção entre vários bancos de dados de baixo uso nos permite toocreate uma solução que também executa e econômica. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Bancos de Dados SQL do Azure ajudam a colocar dados em contêiner para isolamento e segurança
Banco de dados SQL do Azure permite SnelStart tooeasily e mover tooAzure de dados de administração de empresas de local de clientes de maneira transparente. Olá banco de dados do SQL Azure é um contêiner conveniente que fornece isolamento de um limite para autenticação, autorização e recursos de backup e restauração fácil. Os bancos de dados fornecem um modelo conceitual bastante adequado para a administração dos negócios. Acordo tooCarlo Kuip, arquiteto de TI "itens dentro de limites esse contêiner contém dados confidenciais é crucial tooa business e armazenar esses itens em um mantém isolado do banco de dados-los bem protegidos. Podemos gerenciar autorização em nível de banco de dados Olá e até mesmo automatizar horizontal desses bancos de dados e gerenciamento de saudação sem a necessidade de administradores de banco de dados (DBAs) em sua equipe."

SQL Data Warehouse do Azure também desempenha um papel em matéria de segurança e gerenciamento de SnelStart hello, ajudando a empresa Olá coletar dados de telemetria, como detecção de intrusões, o log de atividades do usuário e conectividade.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>O Azure remove a sobrecarga para que os desenvolvedores possam passar mais tempo agregando valor
modelo de plataforma do Azure Olá removido sobrecarga de infraestrutura e habilitado SnelStart tooautomate implantações usando bibliotecas de gerenciamento do c#. Como os estados de Kuip, "foi capaz de toogrow opções nossas operações atuais com uma equipe muito pequena ao simultaneamente cada vez maior escalabilidade, velocidade e recuperação de desastres para os clientes. desenvolvimento de tooservices shift Olá liberados recursos toofocus em novos serviços e recursos, em vez de apenas atualizar tookeep de código existente para cima com novos códigos de normas ou imposto." Ele adiciona, "Automatizar o gerenciamento e usando a oferta de SaaS hello, estamos capaz de toodeliver mais valor para nossos clientes, sem ter que toomake grandes investimentos em equipe operacional." Por exemplo, por meio do Azure e Elásticos pools, SnelStart foi capaz de tooadd uma variedade de recursos novos, incluindo a integração de dados do cliente mais robusta com bancos, cobrança novos serviços, as verificações de plano de fundo de pequenas empresas e serviços de email.

> "Hello apenas primeiros meses de 2016, é expandido nosso implantações do banco de dados SQL de toomore 5.500 cerca de 12.000 e estamos atualmente adicionando cerca de 1.000 bancos de dados por mês."
> 
> — Henry Been, arquiteto de software
> 
> 

Gerenciamento de banco de dados é ainda mais automatizado com recurso de trabalhos Elástico hello. Como Kuip estados, "altamente Agradecemos a descoberta automática de bancos de dados em uma instância do banco de dados SQL [server] hello." Isso permite SnelStart tooexecute operações de gerenciamento entre seu cliente dinamicamente crescente base sem sobrecarga adicional.

A SnelStart também está desenvolvendo uma API que atua como um agente entre os dados dos clientes e os aplicativos criados por parceiros de software terceirizados. Como os estados de Kuip, "essa API permite que software de tooour outros fornecedores tooadd funcionalidade, como eliminar entrada de dados para faturas e outros documentos." Os clientes não terão mais toomanually faturas de tipo em seu software de contabilidade de pequenas empresas; Olá SnelStart software trocam informações necessárias Olá diretamente. Isso permite que os clientes toojoin tarefas de administração seu negócios com o ecossistema de saudação de informações é emergentes da transformação digital no setor de saudação.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Como os serviços do Azure habilitam o SaaS para a SnelStart
Usando o Azure, SnelStart pode atender a seus clientes e seus contadores mais diretamente na nuvem de saudação. Por exemplo, clientes e contadores podem compartilhar informações diretamente acessando a API do cliente SnelStart, hospedado no Azure. Estados de Kuip, "esses serviços reutilizáveis estão disponíveis tooour voltadas para o cliente web apps, e fornecem infraestrutura e as funções comuns tooallow administração de toobusiness de acesso para clientes e software de terceiros toothird usado pelos clientes. Exemplos incluem o fornecimento de recursos de configuração de produto, gerenciamento de regras de firewall e gerenciamento de processos de execução longa, como backups".

> Nosso objetivo é tooprovide 100 por cento automação de serviços de administração de negócios para nossos clientes." 
> 
> — Carlo Kuip, arquiteto de TI
> 
> 

Além disso, os serviços da web SnelStart permitem que clientes e contadores tooeasily acessar dados em pools Elásticos do banco de dados SQL. Esse modelo de SaaS, aliado à elasticidade do banco de dados e ao Azure Resource Manager, fornece a SnelStart recursos de escalabilidade que complementam cada implantação do Azure. implementação de saudação é totalmente automatizada usando bibliotecas de gerenciamento do c#.

![Arquitetura da SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Figura 1. Desde junho de 2016, a SnelStart tem mais de 11.000 bancos de dados e mais de 50 pools elásticos

## <a name="simplicity-from-hello-cloud"></a>Simplicidade da nuvem de saudação
A mudança tooan solução baseada em nuvem do Azure, SnelStart foi toosupport capaz de crescimento de cliente rápida, oferecendo serviços e recursos inovadores. TooBeen, de acordo com "com o Azure, podemos fornecer atualizações quase contínua para nossos clientes, sem expandir nossa equipe de operações. E obtemos Olá todos os outros ótimos recursos do Azure — como escalabilidade e recuperação de desastres — incluídos na. "

> "Quando foi realmente sobre em Redmond... Recebi uma chamada de um desenvolvedor em países baixos hello, transmita para me sobre um problema específico. Podemos foi capaz de tooget Microsoft toodeliver uma alteração em seu ambiente de produção dentro de 48 horas toosolve nosso problema. "
> 
> — Henry Been, arquiteto de software
> 
> 

SnelStart também agradece sua parceria forte hello, que eles desenvolveu com a equipe de banco de dados SQL do Microsoft Azure hello. Como os estados de Kuip "temos discussões sobre os recursos e como a tecnologia toouse, que é algo aconselhável em ambos os lados."
objetivo imediato saudação SnelStart é tookeep aumentando seu cliente satisfeito base. Como foi estados, "Sem hello técnica e limitações de recursos que tivemos como um ISV, não há nenhum toohow limite agora podemos aumentar".

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre pools Elásticos do Azure, consulte [pools Elásticos](sql-database-elastic-pool.md).
* toolearn mais informações sobre funções Web e funções de trabalho, consulte [funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais sobre o Azure SQL Data Warehouse, consulte [SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn mais sobre SnelStart, consulte [SnelStart](http://www.snelstart.nl).

