---
title: aaaDeploy toohello sua oferta do Azure Marketplace | Microsoft Docs
description: "Saiba mais sobre e percorrer Olá instruções toodeploy sua oferta — a imagem de máquina virtual, serviço de desenvolvedor, o serviço de dados, etc. – toohello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Implantar toohello sua oferta do Azure Marketplace
Quando estiver satisfeito com sua oferta (ou seja, testar cenários de clientes, marketing conteúdo, etc.) e você está pronto toolaunch, solicitação **Push tooproduction** em Olá **publicar** guia.  

1. Olá quatro etapas na página de instruções passo a passo de saudação em Olá portal de publicação deve ser concluída e verde. Ofertas de máquina Virtual, certifique-se de que Olá diretrizes a seguir são seguidas.
   
    ![desenho][img-pubportal-walkthru-checked]
2. Selecione Olá **publicar** guia na lista Olá Olá lado esquerdo.
   
    ![desenho][img-pubportal-menu-publish]
3. Botão Olá **solicitar aprovação toopush tooproduction**. Quando é feita a solicitação de Olá, equipe de aprovação de saudação executa uma análise final e, em seguida, sua oferta estará disponível em hello Azure Marketplace.
   
    ![desenho][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> No caso de máquinas virtuais, quando você clicar em Olá botão solicitação de aprovação toopush tooproduction, Olá etapas a seguir é executada por trás da cena hello. Você será tooview capaz de andamento de saudação de cada etapa na guia publicação Olá Olá portal de publicação. Você deve verificar essa página em intervalos regulares (até que o status de saudação mostra "Listados") para obter quaisquer informações de falha que precisam de correção do seu final.
> 
> * No primeiro sua solicitação de produção entra toohello equipe de certificação que validar Olá vhd. No entanto, se você estiver atualizando sua oferta já listada e solicitação Olá tem somente alterações de marketing, em seguida, Olá certificação etapa será ignorada.
> * Na próxima etapa de hello, solicitação Olá vir toohello equipe de validação de conteúdo que verificar Olá conteúdo de oferta de saudação de marketing.
> * Se Olá acima etapas forem bem-sucedidas, oferta Olá for aprovada em produção. Neste momento, Olá status se tornar "listado" no portal de publicação hello. No entanto, esse status de "Listados" não implica que o processo de saudação foi concluído. Olá, seguindo as etapas necessidade toobe concluído antes de oferta de saudação está disponível no hello Azure Marketplace.
> * Após a aprovação de oferta de saudação em produção na etapa de saudação acima, a replicação inicial de oferta Olá em todos os Olá datacenters do Azure. Ele geralmente leva 24-48hours para Olá replicação toocomplete mas pode levar até semana tooa dependendo do tamanho de saudação do vhd de saudação. No entanto, se você estiver atualizando sua oferta já listada e tem somente alterações de marketing, replicação de saudação é mais rápida.
> * Quando a replicação Olá for concluída, oferta Olá estarão disponível em hello Azure Marketplace.
> 
> Você sempre pode excluir oferta Olá enquanto ele está em um **rascunho** status (ou seja, nunca **Push toostaging** ou **Push tooproduction**). Em Olá **histórico** , clique em Olá **Descartar rascunho** botão na parte inferior de saudação do hello página toodelete um rascunho.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Lista de verificação de produção para todas as ofertas de Máquina Virtual
* Você deve ser um parceiro certificado do Microsoft Azure
* Na guia de SKUs hello, opção hello "Ocultar este SKU de saudação Marketplace porque sempre deve ser comprado por meio de um modelo de solução" deve ser marcado como Sim somente se Olá SKU é uma parte de um modelo de solução. Em todos os Olá outros casos, essa opção sempre deve ser marcada como não.
* Lembre-se: Você não deve alterar configuração de visibilidade SKU de saudação quando Olá SKU está listado. Não oferecemos suporte a essa funcionalidade.
* Certifique-se de logotipos Olá aderem diretrizes de logotipo do Azure Marketplace toohello indicadas abaixo.
* As descrições da oferta e da SKU não devem ser iguais.
* O título da SKU e o resumo longo da oferta não devem ser iguais.
* O título da SKU e o resumo da oferta não devem ser iguais.
* Os títulos das SKUs não devem ser idênticos para uma oferta com várias SKUs.

**Diretrizes de logotipo do Azure Marketplace**

* Olá design do Azure tem uma paleta de cores simples. Mantenha baixo número de saudação do primário e secundário cores no logotipo.
* cores de tema de saudação do hello portal do Azure são brancas e preto. Portanto, evite usar essas cores da cor de plano de fundo de saudação do seu logotipos. Use cor que tornem seus logotipos proeminente no portal do Azure de saudação. É recomendável usar cores primárias simples. Se você estiver usando o plano de fundo transparente, certifique-se de que Olá texto do logotipo não é branco ou preto.
* Não use um plano de fundo do gradiente no logotipo hello.
* Evite colocar o texto, mesmo em sua empresa ou nome de marca, no logotipo hello.
* Olá aparência de seu logotipo deve ser 'simples' e deve evitar gradientes.
* logotipo de saudação não deve ser estendido.

**Diretrizes adicionais para o logotipo de herói hello:**

* logotipo do Hello herói é opcional. publicador de saudação pode escolher não tooupload um logotipo herói. **No entanto, uma vez carregado ícone herói de saudação não pode ser excluída da saudação portal de publicação. Nesse momento, parceiro Olá deve seguir as diretrizes do Azure Marketplace Olá ícones herói outra oferta de saudação não serão tooproduction aprovado.**
* Olá, nome de exibição do publicador, hello e título do SKU oferecem resumo longo são exibidos na cor branca. Portanto, você deve evitar manter qualquer cor clara no plano de fundo de saudação do hello herói ícone. Planos de fundo pretos, brancos e transparentes não são permitidos para ícones Hero.
* Olá nome de exibição do publicador, SKU título, resumo longo de oferta hello e Olá criar botão são inserido programaticamente no logotipo de herói Olá depois que a oferta Olá vai listada. Portanto você não deve inserir qualquer texto enquanto você estiver criando o logotipo de herói hello. Deixe espaço vazio direita Olá porque texto hello (ou seja, o nome de exibição do Editor, título da SKU, resumo longo de oferta de saudação) será incluído programaticamente por nós ali. um espaço vazio para o texto de saudação Olá deve ser 415 x 100 em Olá direito (e ele tem um deslocamento de 370px da saudação esquerda).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Lista de verificação adicional de produção para ofertas de VM já listadas
* Verifique se já houver uma oferta com hello mesmo oferecem o nome de sua empresa. Se Sim, você deve adicionar uma nova versão do hello SKU na oferta de saudação existente em vez de criar uma nova oferta duplicada.
* Disco de dados não deve alterar entre duas versões de saudação mesmo SKU.
* Hello Azure Marketplace não oferece suporte a alteração da saudação de preços listados SKUS como ele afeta a cobrança de clientes existentes Olá Olá. Certifique-se de que você não altere Olá preços de SKUs Olá listado em regiões Olá onde Olá SKU está disponível. No entanto, você pode adicionar novos SKUs ou adicionar novos tooan regiões existentes SKU.

## <a name="next-steps"></a>Próximas etapas
Depois que a oferta de saudação fica ativo, teste Olá toovalidate de cenários de cliente que todos os contratos de saudação e funcionalidade funcionam corretamente no ambiente de produção de hello como ambiente de preparo Olá testadas e validadas no.

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
