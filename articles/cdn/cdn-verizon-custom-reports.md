---
title: "Relatórios personalizados da Verizon | Microsoft Docs"
description: "É possível exibir os padrões de uso da CDN usando os seguintes relatórios: largura de banda, dados transferidos, ocorrências, status do cache, taxa de ocorrências no cache, dados IPV4/IPV6 transferidos."
services: cdn
documentationcenter: 
author: dksimpson
manager: 
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/11/2017
ms.author: v-deasim
ms.openlocfilehash: f09195dc07a96ebcca7f7a9e4bcf521fae13630c
ms.sourcegitcommit: 7f1ce8be5367d492f4c8bb889ad50a99d85d9a89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="custom-reports-from-verizon"></a>Relatórios personalizados da Verizon

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Ao usar relatórios personalizados de Verizon via Portal de gerenciamento para perfis Verizon, você pode definir o tipo de dados a serem coletados para relatórios de borda de CNAMEs.


## <a name="accessing-verizon-custom-reports"></a>Como acessar Relatórios personalizados da Verizon
1. Na folha do perfil do CDN, clique no botão **Gerenciar** .
   
    ![Botão Gerenciar perfil da CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    O portal de gerenciamento da CDN é aberto.
2. Passe o mouse sobre a guia **Análise**, depois sobre o submenu **Relatórios Principais**. Clique em **CNAMEs de Borda**.
   
    ![Portal de gerenciamento da CDN – Menu Relatórios personalizados](./media/cdn-reports/cdn-custom-reports.png)

## <a name="edge-cnames-custom-report"></a>Relatório personalizado de CNAMEs de borda
O relatório personalizado de CNAMEs de borda fornece ocorrências e estatísticas de dados transferidos para CNAMEs de borda em que o log de relatório personalizado foi habilitado. CNAMEs de borda consistem em nomes de host de ponto de extremidade de CDN do Azure e quaisquer nomes de host de domínio personalizados associados. 

O log de dados de relatório personalizado se inicia uma hora depois de você habilitar a funcionalidade de geração de relatórios personalizados de CNAMEs de borda. Você pode exibir dados de relatório por meio da geração de um relatório de CNAMEs de borda para uma plataforma específica ou para todas as plataformas. A cobertura desse relatório é limitada aos CNAMEs de borda para os quais foram coletados dados de relatório personalizado durante o período de tempo especificado. O relatório de CNAMEs de borda consiste em uma tabela de dados e grafos para os 10 principais CNAMEs de borda de acordo com a métrica definida na opção Métrica. 

Gere um relatório personalizado definindo as seguintes opções de relatório:

- Métrica: as seguintes opções contam com suporte:

   - Ocorrências: indica o número total de solicitações direcionadas para um CNAME de borda em que a funcionalidade de geração de relatório personalizado está habilitada. Essa métrica não inclui o código de status retornado ao cliente.

   - Dados transferidos: indica a quantidade total de dados transferidos dos servidores de borda para os clientes HTTP (por exemplo, navegadores da Web) para solicitações direcionadas a um CNAME de borda no qual a funcionalidade de geração de relatório personalizado está habilitada. A quantidade de dados transferidos é calculada adicionando cabeçalhos de resposta HTTP ao corpo da resposta. Como resultado, a quantidade de dados transferidos para cada ativo é maior que o tamanho do arquivo real.

- Agrupamentos: determina o tipo das estatísticas que são mostradas abaixo do gráfico de barras. Há suporte para as seguintes opções:

   - Códigos de resposta HTTP: organiza as estatísticas por código de resposta HTTP (por exemplo, 200, 403, etc.) retornado ao cliente. 

   - Status do cache: organiza as estatísticas por status de cache.


Para definir o intervalo de datas do relatório, é possível selecionar um intervalo de datas predefinido na lista suspensa, como **Hoje** ou **Esta semana**, ou selecionar **Personalizado** e inserir manualmente um intervalo de datas clicando nos ícones de calendário. 

Depois de selecionar o intervalo de datas, clique em **Ir** para gerar o relatório.

Você pode exportar os dados em formato Excel clicando no símbolo do Excel à direita do botão **Ir**.

![Relatório de CNAMs](./media/cdn-reports/cdn-cnames-report.png)

## <a name="edge-cnames-custom-report-fields"></a>Campos de relatório personalizado de CNAMEs de borda

| Campo                     | Descrição   |
|---------------------------|---------------|
| 2xx                       | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status HTTP do tipo 2xx (por exemplo, 200 OK). |
| 3xx                       | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status HTTP do tipo 3xx (por exemplo, 302 Encontrado ou 304 Não modificado). |
| 4xx                       | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status HTTP do tipo 4xx (por exemplo, 400 Solicitação incorreta, 403 Proibido ou 404 Não encontrado). |
| 5xx                       | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status HTTP do tipo 5xx (por exemplo, 500 Erro interno do servidor ou 502 Gateway incorreto). |
| Porcentagem de ocorrências no cache               | Indica a porcentagem de solicitações armazenáveis em cache que foram fornecidas diretamente do cache para o solicitante. |
| Acertos do Cache                | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em uma ocorrência no cache (por exemplo, TCP_EXPIRED_HIT, TCP_HIT ou TCP_PARTIAL_HIT). Uma ocorrência no cache acontece quando é encontrada uma versão em cache do conteúdo solicitado. |
| Dados transferidos (MB)     | Indica a quantidade total de dados transferidos (MB) de servidores de borda para clientes HTTP (navegadores da Web) do CNAME de borda. A quantidade de dados transferidos é calculada adicionando os cabeçalhos de resposta HTTP ao corpo da resposta. Como resultado, a quantidade de dados transferidos para cada ativo é maior que o tamanho do arquivo real. |
| Descrição               | Identifica um CNAME de borda pelo seu nome de host |
| Acertos                      | Indica o número total de solicitações para o CNAME de borda |
| Perdas                    | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em uma perda no cache (por exemplo, TCP_CLIENT_REFRESH_MISS, TCP_EXPIRED_MISS ou TCP_MISS). Uma perda no cache ocorre quando o conteúdo solicitado não foi armazenado em cache no servidor de borda que cumpriu a solicitação. | 
| Sem cache                  | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status do cache do tipo CONFIG_NOCACHE.  |
| outro                     | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda indicado, que resulta em um código de status HTTP fora do intervalo 2xx–5xx. |
| Plataforma                  | Indica a plataforma que trata do tráfego do CNAME de borda. |
| Não atribuído               | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda para o qual as informações do código de status do cache ou do código de status HTTP não foram registradas.  |
| Não armazenável em cache               | Indica o número total de solicitações ou dados transferidos (MB) para o CNAME de borda, que resulta em um código de status do cache do tipo UNCACHEABLE.  |


## <a name="considerations"></a>Considerações
Os relatórios só podem ser gerados dentro dos últimos 18 meses.

