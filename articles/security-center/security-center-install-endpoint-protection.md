---
title: "aaaInstall proteção de ponto de extremidade na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * instalar Endpoint Protection * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Instalar o Endpoint Protection na Central de Segurança do Azure
A Central de Segurança do Azure recomenda que você instale a proteção de ponto de extremidade nas VMs (máquinas virtuais) do Azure caso ainda não esteja habilitada. Essa recomendação se aplica somente a máquinas virtuais tooWindows.

> [!NOTE]
> Esta implantação de exemplo usa o Microsoft Antimalware. Consulte a [Integração de parceiro na Central de Segurança do Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) para obter uma lista de parceiros integrados com a Central de Segurança.  
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Este documento não é um guia passo a passo.
>
>

1. Em Olá **recomendações** folha, selecione **instalar o Endpoint Protection**.
   ![Selecione Instalar o Endpoint Protection][1]
2. Olá **instalar o Endpoint Protection** folha é aberta exibindo uma lista de máquinas virtuais sem proteção de ponto de extremidade. Selecione Olá Olá de lista VMs que você deseja tooinstall proteção de ponto de extremidade em e clique em **instalar nas máquinas virtuais**.
   ![Selecione VMs tooinstall Endpoint Protection no][2]
3. Olá **selecione Endpoint Protection** folha abre tooallow você tooselect Olá endpoint protection solução desejada toouse. Neste exemplo, vamos selecionar **Antimalware da Microsoft**.
   ![Selecionar Endpoint Protection][3]
4. Informações adicionais sobre solução de proteção de ponto de extremidade de saudação são exibidas. Selecione **Criar**.
   ![Criar solução antimalware][4]
5. Insira configurações Olá necessárias no hello **Adicionar extensão** folha e, em seguida, selecione **Okey**. toolearn mais sobre configurações hello, consulte [padrão e a configuração de Antimalware personalizada](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[O Antimalware da Microsoft](../security/azure-security-antimalware.md) está ativo no hello selecionado VMs.

## <a name="see-also"></a>Consulte também
Este artigo lhe mostrou como tooimplement Olá recomendação da Central de segurança "Instalar o Endpoint Protection." toolearn mais sobre como habilitar o Antimalware da Microsoft no Azure, consulte Olá documento a seguir:

* [O Antimalware da Microsoft para serviços de nuvem e máquinas virtuais](../security/azure-security-antimalware.md) – Saiba como toodeploy Antimalware da Microsoft.

toolearn mais sobre o Centro de segurança, consulte Olá documentos a seguir:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
