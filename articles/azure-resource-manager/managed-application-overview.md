---
title: aplicativos gerenciados do aaaOverview do Azure | Microsoft Docs
description: "Descreve os conceitos de saudação do Azure aplicativos gerenciados"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Visão geral de aplicativos gerenciados do Azure

Os fornecedores que usam o Azure podem oferecer soluções toocustomers em torno de Olá, mundo. O Azure Marketplace é uma galeria composta por centenas de modelos complexos com vários recursos próprios e de terceiros. Em questão de minutos, os clientes podem implantar e começar a usar aplicativos PaaS (plataforma como serviço) e SaaS (software como serviço). 

Embora Olá Marketplace fornece uma ótima maneira para os clientes tooquickly implantar uma oferta, Prezado cliente é responsável por manter e atualizar solução hello. Além de cobrança de imagem de máquina virtual hello, fornecedores não podem cobrar os clientes para uso de saudação de um aplicativo. Além disso, os fornecedores não podem impedir os clientes de modificar recursos essenciais de aplicativos. Fornecedores também não é possível bloquear propriedade toointellectual de acesso que compõe um aplicativo. Os aplicativos gerenciados do Azure fornecem soluções para esses problemas. 

Um aplicativo gerenciado é modelo de solução de tooa semelhante em Olá Marketplace, com uma diferença importante. Em um aplicativo gerenciado, recursos de saudação são provisionados tooa grupo de recursos que é gerenciado pelo fornecedor de saudação. grupo de recursos de saudação está presente na assinatura saudação do cliente, mas uma identidade no locatário do fornecedor Olá tem grupo de recursos de toohello de acesso.

## <a name="advantages-of-managed-applications"></a>Vantagens dos aplicativos gerenciados

Provedores de serviço (MSPs), ISVs, gerenciados e as equipes de TI centrais corporativas podem usar soluções de toodeliver aplicativos gerenciados por meio de saudação Marketplace ou Olá catálogo de serviços. Embora os clientes implantar esses aplicativos gerenciados em suas assinaturas, eles não têm toomaintain, atualizar ou atender. Como fornecedores de gerenciarem e oferecer suporte a aplicativos de hello, os clientes não tem toomanage de dados de conhecimento do domínio de aplicativo específico toodevelop esses aplicativos. Os clientes automaticamente podem adquirir atualizações de aplicativo sem Olá necessidade tooworry sobre solução de problemas e diagnosticar problemas com aplicativos de saudação.

Para fornecedores e provedores, aplicativos gerenciados criam uma infraestrutura de toosell de canal e o software por meio de saudação Marketplace. Aplicativos gerenciados também fornecem uma maneira tooattach serviços e suporte operacional tooAzure clientes. Fornecedores podem cobrar os clientes usando Olá sistema de cobrança do Azure. Eles podem usar modelos toomanage saudação do ciclo de vida dos aplicativos implantados. Essas soluções são independentes e sealed toohello cliente, para que fornecedores possam fornecer o serviço de alta qualidade. Essa abordagem beneficia fornecedores de PaaS e SaaS. Ele também ajuda as equipes de plataforma central corporativa e integradores de sistema (SIs) que deseja toopackage e revender suas soluções.

## <a name="managed-application-types"></a>Tipos de aplicativos gerenciados
Os aplicativos gerenciados do Azure vêm em dois tipos: Catálogo de Serviços e Marketplace.
 
### <a name="service-catalog"></a>Catálogo de Serviços  

Com hello catálogo de serviços, os clientes podem criar um catálogo de soluções aprovados para o Azure toobe usados por pessoas em sua organização. Manter esse catálogo de soluções é útil para as equipes de TI centrais em empresas. Eles podem usar Olá catálogo tooensure cumprimento determinados padrões organizacionais que fornecem soluções para suas organizações. Elas podem controlar, atualizar e realizar a manutenção desses aplicativos. Os funcionários podem usar Olá catálogo tooeasily descobrir conjunto avançado de saudação de aplicativos que são recomendados e aprovada por seu departamento de TI. Os clientes Consulte aplicativos de catálogo de serviços gerenciados de saudação que criaram. Eles também podem ver Olá aplicativos gerenciados que outras pessoas na organização parcela com eles.
 
Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).
 
Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Aplicativos gerenciados estão disponíveis por meio de saudação Marketplace em Olá portal do Azure. Depois de fornecedor Olá publica esses aplicativos, elas estão disponíveis para todas as pessoas dentro ou fora de uma organização tooconsume. Com essa abordagem, MSPs, ISVs e SIs podem oferecer tooall suas soluções do Azure aos clientes. Os clientes obtêm benefício de saudação de usar essas soluções complexas sem Olá necessidade tooinvest compreensão e manutenção Olá soluções. 

Atualmente, os publicadores podem disponibilizar suas ofertas como um aplicativo gerenciado ou um modelo de solução não gerenciado. Olá principais componentes da publicação de um aplicativo gerenciado incluem o arquivo de modelo de saudação e o arquivo de definição de interface do usuário de saudação. arquivo de modelo Olá descreve recursos de saudação que são provisionados. arquivo de definição de interface do usuário Olá descreve como Olá necessário entradas para provisionar esses recursos são exibidas no portal de saudação. Olá necessário arquivos são empacotados em um arquivo. zip e carregados por meio do portal de publicação hello.
 
Para obter informações sobre como publicar um aplicativo gerenciado de toohello Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).

Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Principais conceitos

### <a name="managed-resource-group"></a>Grupo de recursos gerenciado
Olá grupo de recurso gerenciado é onde tudo hello Azure recursos que são provisionados no modelo de saudação são criados. Por exemplo, se o dispositivo Olá toocreate usada uma conta de armazenamento, esse grupo de recursos contém recurso de conta de armazenamento hello. Ele não contém recursos de dispositivo de saudação.

### <a name="appliance-package"></a>Pacote de dispositivo
publicador de saudação cria um pacote que contém os arquivos de modelo hello e arquivo de createUIDefinition de saudação. Especificamente, ele contém Olá seguintes arquivos:

- **applianceMainTemplate.json**: este arquivo de modelo define todos os recursos de saudação provisionados pelo dispositivo hello. Esse arquivo é um arquivo de modelo regular que usou toocreate recursos.

- **MainTemplate.json**: este arquivo de modelo define o recurso de dispositivo de saudação (Microsoft.Solutions/appliances). Uma propriedade essencial definida neste recurso é o ManagedResourceGroupId. Essa propriedade indica qual grupo de recursos é usado toohost Olá recursos reais que são definidos em applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: esse arquivo descreve como saudação da interface do usuário necessário para parâmetros de saudação definidos no modelo de saudação é renderizada.

### <a name="authorization"></a>Autorização
publicador Olá deve especificar permissões Olá exigidas por recursos de Olá Olá fornecedor toomanage em nome do cliente hello. Essa permissão se aplica a toohello grupo de recurso gerenciado. Saudação de conjunto de valores a seguir:

- **PrincipalID**: Olá identificador do Azure Active Directory (AD do Azure) do hello usuário, grupo ou aplicativo que tenha usado o grupo de recurso gerenciado toogrant acesso toohello. Esse identificador pertence locatário toohello do publicador.

- **RoleDefinitionID**: Olá identificador do AD do Azure da saudação função atribuída toohello anterior a ID da entidade. Pode ser qualquer uma das funções internas de controle de acesso baseado em função hello no locatário do publicador hello. Para saber mais, consulte [Funções internas para Controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Próximas etapas

* Para obter informações sobre publicação aplicativos gerenciados toohello Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).
* Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).
* Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).
* Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).
* toocreate um arquivo de definição de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
