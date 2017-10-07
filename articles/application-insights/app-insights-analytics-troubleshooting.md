---
title: "aaaTroubleshoot análise no Insights de aplicativo do Azure | Microsoft Docs"
description: 'Problemas com a Application Insights Analytics? Comece por aqui. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Solução de problemas do Analytics no Application Insights
Problemas com a [Application Insights Analytics](app-insights-analytics.md)? Comece por aqui. A análise é Olá poderosa ferramenta de pesquisa de informações de aplicativo do Azure.

## <a name="limits"></a>limites
* No momento, os resultados da consulta são limitado toojust mais de uma semana de dados passados.
* Navegadores em que testamos: edições mais recentes do Chrome, Edge e Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Extensões do navegador incompatíveis conhecidas
* Ghostery

Desabilitar extensão hello, ou use um navegador diferente.

## <a name="e-a"></a> "Erro inesperado"
![Tela de erro inesperado](./media/app-insights-analytics-troubleshooting/010.png)

Ocorreu um erro interno durante o tempo de execução do portal. Exceção sem tratamento.

* Limpe o cache do navegador hello. 

## <a name="e-b"></a>403.... Tente tooreload
![403.... Tente tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso). portal de saudação não pode ter nenhuma maneira muito recuperar sem alterar as configurações do navegador.

* Verifique se [cookies de terceiros são habilitados](#cookies) no navegador de saudação. 

## <a name="authentication"></a>403... verificar zona de segurança
![403... verifique a zona de segurança](./media/app-insights-analytics-troubleshooting/030.png)

Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso). portal de saudação não pode ter nenhuma maneira muito recuperar sem alterar as configurações do navegador.

1. Verifique se [cookies de terceiros são habilitados](#cookies) no navegador de saudação. 
2. Você usou um favorito, o marcador ou o portal da análise de link salvo tooopen Olá? Conectado com credenciais diferentes que você usou quando salvo link Olá?
3. Tente usar uma janela do navegador privada/anônima (depois de fechar todas as janelas desse tipo). Você terá tooprovide suas credenciais. 
4. Abrir outra janela do navegador (comum) e vá muito[Azure](https://portal.azure.com). Saia. Em seguida, abra o link e entrar com as credenciais corretas de saudação.
5. Os usuários do Edge e do Internet Explorer também podem receber esse erro quando não há suporte para as configurações de zona confiável.
   
    Verifique se ambos [portal da análise de](https://analytics.applicationinsights.io) e [portal do Azure Active Directory](https://portal.azure.com) estão em Olá mesma zona de segurança:
   
   * No Internet Explorer, abra **Opções da Internet**, **Segurança**, **Sites Confiáveis**, **Sites**:
     
     ![Caixa de diálogo Opções da Internet, adição de um site tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     Na lista de sites hello, se qualquer uma das seguintes URLs de saudação são incluídos, certifique-se que Olá outros também estão incluídos:
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Recurso não encontrado
![404... recurso não encontrado](./media/app-insights-analytics-troubleshooting/040.png)

O recurso de aplicativo foi excluído do Application Insights e não está mais disponível. Isso pode acontecer se você salvou a página de análise de toohello Olá URL.

## <a name="e-e"></a>403 ... Sem autorização
![403 ... não autorizado](./media/app-insights-analytics-troubleshooting/050.png)

Você não tem permissão tooopen esse aplicativo na análise.

* Você obteve Olá link de outra pessoa? Solicite toomake certeza Olá [colaboradores para este grupo de recursos ou leitores](app-insights-resources-roles-access-control.md).
* Você salvou link hello usando credenciais diferentes? Olá abrir [portal do Azure](https://portal.azure.com), sair e, em seguida, tente novamente, esse link fornecer as credenciais corretas de saudação.

## <a name="html-storage"></a>403 ... Armazenamento HTML5
Nosso portal usa sessionStorage e localStorage do HTML5.

* Chrome: configurações, privacidade, configurações de conteúdo.
* Internet Explorer: Opções da Internet, guia Avançado, Segurança, Habilitar o armazenamento DOM

![403... Tente armazenamento tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Assinatura não encontrada
![404 ... Assinatura não encontrada](./media/app-insights-analytics-troubleshooting/070.png)

Olá URL é inválida. 

* Abrir o recurso de aplicativo hello em [portal do Application Insights](https://portal.azure.com). Em seguida, use o botão de análise de saudação.

## <a name="e-h"></a>404... a página não existe
![404 ... A página não existe](./media/app-insights-analytics-troubleshooting/080.png)

Olá URL é inválida.

* Abrir o recurso de aplicativo hello em [portal do Application Insights](https://portal.azure.com). Em seguida, use o botão de análise de saudação.

## <a name="cookies"></a>Habilitar cookies de terceiros
  Consulte [como toodisable terceiros cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mas observe é preciso muito**habilitar** -los.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

