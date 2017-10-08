---
title: aaaManage sua primeira API no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocreate APIs, operações de adicionar e introdução ao gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Gerenciar sua primeira API no Gerenciamento de API do Azure
## <a name="overview"> </a>Visão geral
Este guia mostra como tooquickly começar a usar o gerenciamento de API do Azure e fazer sua primeira chamada de API.

## <a name="concepts"> </a>O que é o Gerenciamento de API do Azure?
Você pode usar o gerenciamento de API do Azure tootake qualquer back-end e iniciar um programa de API totalmente desenvolvido com base nele.

Cenários comuns incluem:

* **Proteção de infraestrutura móvel** com a retenção de acesso às chaves de API, impedindo ataques DOS ao usar limitação ou políticas avançadas de segurança como validação de token JWT.
* **Habilitando ecossistemas de parceiro ISV** , oferecendo a integração de parceiro rápida por meio de desenvolvedor Olá portal e criação de um toodecouple de fachada de API de implementações internas que não são pronta para consumo do parceiro.
* **Executando um programa de API interno** , oferecendo um local centralizado para Olá organização toocommunicate sobre a disponibilidade de saudação e mais recentes alterações tooAPIs, retenção de acesso com base em contas organizacionais, todas baseadas em um canal protegido entre Olá gateway de API e Olá back-end.

sistema de saudação é composto de saudação componentes a seguir:

* Olá **gateway API** é o ponto de extremidade de saudação que:
  
  * Aceita chamadas de API e roteia tooyour back-ends.
  * Verifica chaves de API, tokens JWT, certificados e outras credenciais.
  * Impõe o uso de cotas e limites de taxa.
  * Transforma sua API Olá imediatamente sem modificações no código.
  * Armazena respostas de back-end em cache em que a instalação.
  * Registra logs de metadados de chamadas para fins de análise.
* Olá **portal do publicador** é a interface administrativa hello, em que você configurar o programa de API. Use-o para:
  
  * Definir ou importar esquema de API.
  * Empacotar APIs em produtos.
  * Configure políticas, como cotas ou transformações em Olá APIs.
  * Obter insights por meio de análises.
  * Gerenciar usuários.
* Olá **portal do desenvolvedor** serve como a presença do Olá web principal para desenvolvedores, onde eles podem:
  
  * Ler a documentação da API.
  * Experimente uma API via console interativo de saudação.
  * Criar uma conta e assinar chaves tooget API.
  * Acessar a análise do seu próprio uso.

## <a name="create-service-instance"> </a>Criar uma instância de Gerenciamento de API
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][Azure Free Trial].
> 
> 

Olá primeira etapa ao trabalhar com gerenciamento de API é toocreate uma instância de serviço. Entrar toohello [Portal do Azure] [ Azure Portal] e clique em **novo**, **Web + móvel**, **gerenciamento de API**.

![Nova instância do Gerenciamento de API][api-management-create-instance-menu]

Para **nome**, especifique um toouse de nome de subdomínio exclusivo para a URL do serviço hello.

Escolha a saudação desejada **assinatura**, **grupo de recursos** e **local** para sua instância de serviço.

Digite **Contoso Ltd.** para Olá **nome da organização**e insira seu endereço de email no hello **email do administrador** campo.

> [!NOTE]
> Este endereço de email é usado para notificações do sistema de gerenciamento de API de saudação. Para obter mais informações, consulte [como tooconfigure notificações e modelos no gerenciamento de API do Azure de email][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Novo serviço de Gerenciamento de API][api-management-create-instance-step1]

As instâncias de serviço de Gerenciamento de API estão disponíveis em três camadas: Developer, Standard e Premium.

> [!NOTE]
> Saudação da camada de desenvolvedor é para o desenvolvimento, testes e programas piloto de API em que a alta disponibilidade não é uma preocupação. Saudação padrão e as camadas Premium, você pode dimensionar seu toohandle de contagem de unidade reservada mais tráfego. as camadas Standard e Premium Olá fornecem o serviço de gerenciamento de API com hello mais potência de processamento e o desempenho. Você pode concluir este tutorial usando qualquer camada. Para obter mais informações sobre as camadas de Gerenciamento de API, confira [Preços de Gerenciamento de API][API Management pricing].
> 
> 

Clique em **criar** toostart sua instância de serviço de provisionamento.

![Novo serviço de Gerenciamento de API][api-management-instance-created]

Depois de criar a instância do serviço hello, próxima etapa de saudação é toocreate ou importar uma API.

## <a name="create-api"> </a>Importar uma API
Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente. Operações de API são serviços da web de tooexisting por proxy.

APIs podem ser criadas (e as operações podem ser adicionadas) manualmente, podendo também ser importadas. Neste tutorial, vamos importar hello API para um serviço da web exemplo Calculadora fornecidos pela Microsoft e hospedados no Azure.

> [!NOTE]
> Para obter orientação sobre como criar uma API e operações de adicionar manualmente, consulte [como toocreate APIs](api-management-howto-create-apis.md) e [como tooadd operações tooan API](api-management-howto-add-operations.md).
> 
> 

APIs são configuradas no portal do publicador hello. tooreach-la, clique em **portal do publicador** na barra de ferramentas de serviço hello.

![Portal do editor][api-management-management-console]

Calculadora de saudação tooimport API, clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importação API**.

![Botão Importar API][api-management-import-api]

Execute Olá etapas tooconfigure Olá Calculadora API a seguir:

1. Clique em **From URL**, digite **http://calcapi.cloudapp.net/calcapi.json** em Olá **URL do documento de especificação** texto caixa e, em seguida, clique em Olá **Swagger**  botão de opção.
2. Tipo **calc** em Olá **sufixo de URL da API da Web** caixa de texto.
3. Clique em Olá **produtos (opcionais)** caixa e escolha **Starter**.
4. Clique em **salvar** tooimport Olá API.

![Adicionar nova API][api-management-import-new-api]

> [!NOTE]
> **Gerenciamento de API** atualmente oferece suporte à versão 1.2 e 2.0 do documento de Swagger para importação. Certifique-se de que, mesmo que a [Especificação Swagger 2.0](http://swagger.io/specification) declare que as propriedades `host`, `basePath` e `schemes` são opcionais, o documento de Swagger 2.0 **PRECISA** conter essas propriedades; caso contrário, não será importado. 
> 
> 

Depois que Olá API é importado, hello página Resumo para a API de saudação é exibida no portal do publicador hello.

![Resumo da API][api-management-imported-api-summary]

Olá seção API tem várias guias. Olá **resumo** guia exibe informações sobre a API de saudação e métricas básicas. Olá [configurações](api-management-howto-create-apis.md#configure-api-settings) guia é usada configuração de Olá tooview e edição de uma API. Olá [operações](api-management-howto-add-operations.md) guia é operações toomanage usado Olá da API. Olá **segurança** guia pode ser usado tooconfigure autenticação de gateway para o servidor de back-end de saudação usando autenticação básica ou [autenticação mútua de certificado](api-management-howto-mutual-certificates.md)e tooconfigure [ autorização do usuário usando o OAuth 2.0](api-management-howto-oauth2.md).  Olá **problemas** guia é tooview usado problemas relatados por desenvolvedores de saudação que estão usando suas APIs. Olá **produtos** guia é usada tooconfigure produtos de Olá que contêm essa API.

Por padrão, cada instância de Gerenciamento de API é fornecida com dois produtos função Web:

* **Inicial**
* **Ilimitado**

Neste tutorial, Olá API de calculadora básica foi adicionado produto de iniciador toohello quando Olá API foi importado.

Na ordem toomake chamadas tooan API, os desenvolvedores devem assinar primeiro produto tooa que lhes dá acesso tooit. Os desenvolvedores podem assinar tooproducts no portal do desenvolvedor hello, ou os administradores podem assinar tooproducts de desenvolvedores no portal do publicador hello. Você é um administrador, desde que você criou instância de gerenciamento de API de saudação em Olá etapas anteriores no tutorial Olá, portanto você já está inscrito tooevery produto por padrão.

## <a name="call-operation"></a>Chamar uma operação do portal do desenvolvedor Olá
Operações podem ser chamadas diretamente no portal do desenvolvedor hello, que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API. Nesta etapa do tutorial, você chamará Olá básica Calculadora API **adicionar dois inteiros** operação. Clique em **portal do desenvolvedor** do menu de saudação à saudação parte superior direita do portal do publicador hello.

![Portal do desenvolvedor][api-management-developer-portal-menu]

Clique em **APIs** no menu superior hello e clique **Calculadora básica** toosee Olá operações disponíveis.

![Portal do desenvolvedor][api-management-developer-portal-calc-api]

Observe as descrições do exemplo hello e parâmetros que foram importados juntamente com hello API e operações, fornecendo a documentação para desenvolvedores de saudação que usará esta operação. Essas descrições também podem ser adicionadas quando as operações são adicionadas manualmente.

Olá toocall **adicionar dois inteiros** operação, clique em **Experimente**.

![Experimente][api-management-developer-portal-calc-api-console]

Insira alguns valores para parâmetros de saudação ou manter Olá padrões e, em seguida, clique em **enviar**.

![HTTP Get][api-management-invoke-get]

Depois que uma operação é invocada, portal do desenvolvedor Olá exibe Olá **status da resposta**, Olá **cabeçalhos de resposta**e qualquer **conteúdo de resposta**.

![Resposta][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Exibir análise
análise tooview para Calculadora básica, portal do publicador switch back toohello selecionando **gerenciar** do menu de saudação à saudação parte superior direita do portal do desenvolvedor hello.

![Gerenciar][api-management-manage-menu]

modo de exibição padrão para o portal do publicador Olá Olá é hello **painel**, que fornece uma visão geral de sua instância de gerenciamento de API.

![Painel][api-management-dashboard]

Passe o mouse sobre o gráfico para Olá Olá **Calculadora básica** métricas específicas do hello toosee de uso de saudação do hello API para um determinado período de tempo.

> [!NOTE]
> Se você não vir todas as linhas do gráfico, alterne o portal do desenvolvedor toohello voltar e fazer algumas chamadas na API de saudação, aguarde alguns instantes e vêm toohello painel.
> 
> 

Clique em **exibir detalhes** tooview Olá página de resumo Olá API, incluindo uma versão maior de métricas de saudação exibida.

![Análise][api-management-mouse-over]

![Resumo][api-management-api-summary-metrics]

Para métricas detalhadas e relatórios, clique em **análise** de saudação **gerenciamento de API** menu Olá esquerda.

![Visão geral][api-management-analytics-overview]

Olá **análise** seção tem Olá quatro guias a seguir:

* **Em um relance** fornece o uso geral e métricas de integridade, bem como Olá melhores desenvolvedores, principais produtos, principais APIs e operações principais.
* **Uso** fornece uma visão mais detalhada das chamadas à API e da largura de banda, incluindo uma representação geográfica.
* **Integridade** abrange os códigos de status, taxas de êxito do cache, tempos de resposta e tempos de resposta de serviço e da API.
* **Atividade** fornece relatórios que fazem busca detalhada sobre a atividade específica Olá pelo desenvolvedor, produto, API e operação.

## <a name="next-steps"> </a>Próximas etapas
* Saiba como muito[proteger sua API com os limites de taxa](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
