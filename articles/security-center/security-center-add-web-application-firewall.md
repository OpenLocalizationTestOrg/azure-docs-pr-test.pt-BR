---
title: "aaaAdd um firewall do aplicativo web na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendações da Central de segurança do Azure * * adicionar um firewall * * de aplicativo de web e * * finalizar a proteção de aplicativo * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Adicionar um Firewall do Aplicativo Web na Central de Segurança do Azure
Central de segurança do Azure pode recomendar que você adicionar um firewall do aplicativo web (WAF) de um toosecure de parceiro Microsoft seus aplicativos web. Este documento orienta você por um exemplo de como tooapply essa recomendação.

Uma recomendação WAF é mostrada para qualquer IP voltado para uso público (IP de nível de instância ou IP de balanceamento de carga) que tem um grupo de segurança de rede associado com portas de entrada da Web abertas (80,443).

Central de segurança recomenda que você provisionar um toohelp WAF se proteger contra ataques direcionados a seus aplicativos web em máquinas virtuais e no ambiente de serviço de aplicativo. Um ASE (Ambiente do Serviço de Aplicativo) é uma opção do plano de serviço [Premium](https://azure.microsoft.com/pricing/details/app-service/) do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo do Azure. toolearn mais sobre ASE, consulte Olá [documentação do ambiente de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Este documento não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **proteger o aplicativo web usando o firewall do aplicativo web**.
   ![Aplicativo Web protegido][1]
2. Em Olá **proteger seus aplicativos da web usando o firewall do aplicativo web** folha, selecione um aplicativo web. Olá **adicionar um Firewall do aplicativo Web** folha é aberta.
   ![Adicione um firewall do aplicativo Web][2]
3. Você pode escolher toouse um firewall do aplicativo web existente se estiver disponível ou você pode criar um novo. Neste exemplo, não existem WAFs disponíveis, por isso vamos criar um novo.
4. toocreate um WAF, selecione uma solução de lista de saudação de parceiros integrados. Neste exemplo, selecionamos **Barracuda Web Application Firewall**.
5. Olá **Firewall do aplicativo Web Barracuda** folha é aberto, fornecendo informações sobre solução de parceiro hello. Selecione **criar** na folha de informações de saudação.

   ![Folha Informações do firewall][3]

6. Olá **novo Firewall do aplicativo Web** folha é aberto, onde você pode executar **configuração da VM** etapas e fornecer **WAF informações**. Selecione **Configuração da VM**.
7. Em Olá **configuração da VM** folha, inserir informações toospin necessário Olá máquina de virtual que executa Olá WAF.
   ![VM configuration][4]
8. Retornar toohello **novo Firewall do aplicativo Web** folha e selecione **WAF informações**. Em Olá **WAF informações** folha, configurar WAF Olá em si. Etapa 7 permite tooconfigure Olá máquina na qual Olá WAF é executado e a etapa 8 permite Olá tooprovision WAF em si.

## <a name="finalize-application-protection"></a>Finalizar a proteção do aplicativo
1. Retornar toohello **recomendações** folha. Uma nova entrada foi gerada depois que você criou WAF hello, chamado **finalizar a proteção do aplicativo**. Essa entrada permite que você saiba o que você precisa que o processo de saudação do toocomplete de ligar Olá WAF dentro Olá rede Virtual do Azure, na verdade, para que ele possa proteger o aplicativo hello.

   ![Finalizar a proteção do aplicativo][5]

2. Selecione **Finalizar a proteção do aplicativo**. Uma nova lâmina é aberta. Você pode ver que há um aplicativo web que precisa toohave seu tráfego redirecionado.
3. Selecione o aplicativo da web hello. Uma folha é aberta e mostra as etapas para concluir a configuração de firewall do aplicativo de web hello. Conclua as etapas de Olá e, em seguida, selecione **restringir o tráfego**. Central de segurança, em seguida, Olá o cabeamento para você.

   ![Restringir o tráfego][6]

> [!NOTE]
> Você pode proteger vários aplicativos web na Central de segurança adicionando esses aplicativos tooyour WAF as implantações existentes.
>
>

logs de saudação do que WAF agora são totalmente integrados. Central de segurança pode iniciar automaticamente coletar e analisar logs de saudação para que ele pode superfície tooyou de alertas de segurança importantes.

## <a name="next-steps"></a>Próximas etapas
Este documento lhe mostrou como tooimplement Olá recomendação da Central de segurança "Adicionar um aplicativo web". toolearn mais sobre como configurar um firewall do aplicativo web, consulte o seguinte hello:

* [Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
