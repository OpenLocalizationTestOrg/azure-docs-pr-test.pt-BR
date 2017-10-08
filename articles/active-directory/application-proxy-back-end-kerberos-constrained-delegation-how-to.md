---
title: "aaaHow tooconfigure um aplicativo de Proxy de aplicativo toouse delegação restrita de Kerberos | Microsoft Docs"
description: "Como tooconfigure delegação restrita de Kerberos para um aplicativo de Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Como tooconfigure um aplicativo de Proxy de aplicativo toouse delegação restrita de Kerberos

Olá métodos disponíveis para a obtenção de SSO toopublished aplicativos podem variar um pouco de tooapplication do aplicativo e uma das opções de saudação que o Proxy de aplicativo do Azure oferece direita sem necessidade de saudação é a delegação restrita de Kerberos (KCD). Isso é onde um host do conector é configurado tooperform restringido de kerberos authentication toobackend aplicativos, em nome dos usuários.

procedimento real de saudação para habilitar o KCD é relativamente simples e normalmente requer não mais do que uma compreensão geral dos Olá vários componentes e fluxo de autenticação que facilita o SSO. Localizando boas fontes de informações toohelp solucionar cenários onde o KCD SSO não funciona conforme o esperado, podem ser esparsas.

Dessa forma, este artigo tenta tooprovide um único ponto de referência que deve ajudar a solucionar e corrigir automaticamente alguns dos problemas mais comuns de saudação que podemos ver. No hello orientações adicionais do mesmo oferta de tempo para diagnosticar hello mais complexo e problemática de implementação.

Observe que este artigo faz Olá seguintes suposições:

-   Proxy de aplicativo do Azure foi implantado como por nossa [documentação](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) e aplicativos de KCD toonon acesso geral está funcionando conforme o esperado.

-   Olá aplicativo de destino publicado baseia-se na implementação do IIS e da Microsoft do kerberos.

-   hosts de servidor e aplicativo Hello residam em um único domínio do Active Directory. Informações detalhadas sobre entre cenários de floresta e de domínio podem ser encontradas em nosso [documento técnico de KCD](http://aka.ms/KCDPaper).

-   Olá assunto aplicativo é publicado em um Azure locatário com pré-autenticação habilitada e os usuários são esperados tooAzure tooauthenticate por meio de formulários de autenticação baseada em. Cenários de autenticação de cliente avançados não são cobertos por este artigo, mas ser adicionados em algum momento no futuro de saudação.

## <a name="prerequisites"></a>Pré-requisitos

Proxy de aplicativo do Azure pode ser implantado em praticamente qualquer tipo de infraestrutura ou arquiteturas de ambiente e hello sem dúvida variam de tooorganization da organização. Uma das causas mais comuns de saudação do KCD relacionados a problemas não são ambientes hello, mas simples configurações incorreta ou supervisão geral.

Por esse motivo, nosso conselho é sempre toostart, certificando-se de ter atendido todos os pré-requisitos Olá dispostos em nosso principal [usando KCD SSO com o artigo de Proxy de aplicativo hello](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) antes de iniciar de solução de problemas.

Particularmente Olá seção Configurar o KCD em 2012R2, pois isso emprega uma abordagem fundamentalmente diferente de tooconfiguring KCD em versões anteriores do Windows, mas também enquanto estiver sendo atento várias outras considerações:

-   Não é incomum um tooopen de servidor membro do domínio uma caixa de diálogo de canal seguro com um controlador de domínio específico. Mova tooanother diálogo a qualquer momento, para que hosts de conector geralmente não devem ser toocommunicate capaz de toobeing restrito com controladores de domínio do site local somente específico.

-   Toohello semelhante acima ponto, entre domínios cenários dependem de referências para direcionam um tooDCs de host do conector que ficam fora do perímetro da rede local de saudação. Nesse cenário, é igualmente importante toomake-se de que também permite tráfego em diante tooDCs que representam a outros domínios do respectivos, caso contrário, a delegação falhar.

-   Sempre que possível, você deve evitar colocar todos os dispositivos IDS/IPS ativos entre hosts de conector e controladores de domínio, pois esses são às vezes intrusivos demais e interferem com o tráfego RPC de núcleo

Quanto gostaríamos tooresolve problemas rapidamente e com eficiência, pode levar tempo, portanto sempre que possível você deve tentar e teste delegação hello mais simples de cenários. Olá mais variáveis que você introduz, hello mais você pode ter toocontend com. Por exemplo, limitar seu teste tooa único conector gastar tempo e conectores adicionais podem ser adicionados depois problemas Olá foi resolvido.

Alguns fatores ambientais podem também estar contribuindo problema tooan, novamente se possível, tente e minimiza Olá arquitetura tooa mínimo para teste. Por exemplo, o firewall interno configurado incorretamente ACLs não são incomuns, portanto, se possível ter todo o tráfego de um conector permitido diretamente por meio de controladores de domínio toohello e aplicativo de back-end. 

Na verdade Olá absoluto melhor lugar tooposition os conectores é fechar como destinos de tootheir como pode ser. Ter um firewall embutido durante testes simplesmente adiciona complexidade desnecessária e apenas pode prolongar as investigações.

Portanto, então o que constitui um problema KCD? Bem, há várias indicações clássicas de SSO KCD com falha e hello sinais primeiro de um problema geralmente se manifestam em Olá navegador.

   ![Erro de configuração do KCD incorreto](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Falha devido a permissões toomissing de autorização](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

todos os que lembre Olá sintoma mesmo falhando tooperform SSO e, consequentemente, negando Olá aplicativo de toohello de acesso do usuário.

## <a name="troubleshooting"></a>Solucionar problemas

Como solucionar, em seguida, dependem de problema hello e observado sintomas. Antes de continuar ainda mais seria sugerimos Olá seguindo os links, pois eles contêm informações úteis que você ainda não pode ter vindo em:

-   [Solucionar problemas e mensagens de erro do Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Sintomas e erros de Kerberos](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Trabalhando com o SSO as identidades locais e na nuvem não são idênticas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Se você tiver isso agora, em seguida, hello principal problema definitivamente existe. Você precisa toodig mais profunda, portanto iniciar separando o fluxo de saudação em três estágios distintos que você pode solucionar problemas.

**Pré-autenticação de cliente** -tooAzure por meio de um navegador de autenticação do usuário externo hello.

Ser capaz de toopre-autenticar tooAzure é obrigatório para KCD SSO toofunction. Isso deverá ser testado e abordado primeiro, se houver algum problema. Observe que a fase de pré-autenticação Olá não tem nenhuma relação tooKCD ou hello aplicativo publicado. Ele deve ser relativamente fácil toocorrect quaisquer discrepâncias por integridade verificar conta de entidade Olá existe no Azure, e que não é desabilitadom/bloqueado. resposta de erro Olá no navegador de saudação é geralmente suficientemente descritivo toounderstand hello. Se você não tiver certeza, você também pode verificar nossos outros tooverify de documentos de solução de problemas.

**Serviço de delegação** -Olá conector de Proxy do Azure obtendo uma kerberos tíquete de serviço de um KDC (Centro de distribuição de Kerberos), em nome dos usuários.

as comunicações externas de saudação entre cliente hello e hello Azure front-end não devem ter nenhuma relevância em KCD natureza, além de garantir que ele funciona. Isso é para que Olá serviço Proxy do Azure pode ser fornecido com uma ID de usuário válida que ser tooobtain usado um tíquete kerberos. Sem isso, KCD não é possível e falharia.

Conforme mencionado anteriormente, mensagens de erro do navegador Olá geralmente fornecem algumas dicas BOM por que as coisas estão falhando. Verifique se toonote Olá ID da atividade e o carimbo de hora em resposta Olá porque isso permite eventos de tooactual toocorrelate Olá comportamento no log de eventos do Proxy do Azure hello.

   ![Erro de configuração do KCD incorreto](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

E Olá Olá vistas log de eventos deve ser visto como eventos 13019 ou 12027 as entradas correspondentes. Você pode encontrar os logs de eventos do conector no hello **Applications and Services Logs** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Conector**&gt;**Admin**.

   ![Evento 13019 do log de eventos do Application Proxy](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Evento 12027 do log de eventos do Application Proxy](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Usar um registro no DNS interno para o endereço do aplicativo hello e não um CName

-   Confirmar novamente a host conector Olá recebeu Olá direitos toodelegate toohello designado SPN da conta de destino e que **usar qualquer protocolo de autenticação** está selecionado. Isso é abordado em nosso [artigo de configuração de SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) principal

-   Verifique se há apenas uma única instância de saudação SPN existente no AD, emitindo um **setspn - x** em um prompt de cmd em qualquer host de membro de domínio

-   Verificar toosee se uma política de domínio está sendo imposta Olá toolimit [tamanho máximo de tokens emitidos kerberos](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), pois esse conector de saudação impedir Obtenha um token se encontrado toobe excessiva

Um rastreamento de rede captura trocas de saudação entre o host do conector hello e um domínio do KDC, em seguida, seria a próxima etapa recomendada Olá na obtenção do mais baixo nível obter detalhes sobre problemas Olá. Você pode encontrar isso no [documento de resolução de problemas para aprofundamento](https://aka.ms/proxytshootpaper).

Se o registro for boa, você verá um evento em logs de saudação informando que a autenticação falhou devido a aplicativo toohello retornando um 401. Isso geralmente indica que esse aplicativo de destino Olá rejeitando seu tíquete, para prosseguir com hello após o próximo estágio.

**Aplicativo de destino** -consumidor Olá de tíquete do kerberos Olá fornecido pelo conector Olá

Esse conector de saudação do estágio é esperado toohave enviado um backend de toohello de tíquete de serviço kerberos, como um cabeçalho na primeira solicitação de aplicativo hello.

-   Usando o aplicativo de hello URL interna definido no portal de hello, validar que o aplicativo hello está acessível diretamente do navegador Olá no host do conector de saudação. Em seguida, você pode fazer logon com êxito. Detalhes sobre como fazer isso podem ser encontrados na página de solução de problemas do conector hello.

-   Ainda no host do conector hello, confirme que a autenticação entre o navegador Olá Olá e aplicativo hello está usando kerberos, seguindo um destes procedimentos hello:

1.  Executar ferramentas de desenvolvimento (**F12**) no Internet Explorer, ou use [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) do host do conector hello. Vá toohello aplicativo usando a URL interna Olá e inspecionar Olá oferecido cabeçalhos de autorização WWW retornados na resposta de saudação do aplicativo hello, tooensure o negotiate ou kerberos está presente. Um blob de kerberos subsequentes retornado na resposta de saudação do hello navegador toohello aplicativos iniciam normalmente com **YII**, portanto, esta é uma boa indicação de kerberos está em execução. NTLM em Olá outro lado sempre começam com **TlRMTVNTUAAB**, que lê NTLMSSP ao decodificar da Base64. Se você vir **TlRMTVNTUAAB** no início de saudação do blob hello, isso significa que o Kerberos é **não** disponíveis. Se você não vê isso, é provável que o Kerberos esteja disponível.

  * Observe que se usar o Fiddler, esse método exigiria desabilitar temporariamente a proteção estendida na configuração do aplicativo hello no IIS.

     ![Janela de inspeção da rede do navegador](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Figura:* uma vez que isso não começa com TIRMTVNTUAAB, este é um exemplo de que o Kerberos está disponível. Este é um exemplo de um Blob de Kerberos que não começa com YII.

2.  Remova temporariamente o NTLM da lista de provedores de saudação no IIS site e acesso de aplicativo diretamente do IE no host de conector. NTLM não mais na lista de provedores de saudação, você deve estar tooaccess capaz de aplicativo de hello usando apenas o Kerberos. Se isso falhar, isso indica que há um problema com a configuração do aplicativo hello e a autenticação Kerberos não está funcionando.

Se Kerberos não estiver disponível, a autenticação do aplicativo de verificação Olá negociam as configurações no IIS toomake-se de que é listada mais alto, com NTLM apenas abaixo dela. (Não Negotiate: kerberos ou Negotiate: PKU2U). Só continue se Kerberos está funcional.

   ![Fornecedores de autenticação do Windows](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Com o Kerberos e NTLM no lugar, permite agora desabilitar temporariamente a pré-autenticação para o aplicativo hello no portal de saudação. Veja se você pode acessá-lo de saudação à internet usando a URL externa de saudação. Você deve ser tooauthenticate solicitada e deve ser capaz de toodo para Olá mesmo conta Olá usado em etapa anterior. Caso contrário, isso indica um problema com o aplicativo de back-end hello e não KCD afinal.

-   Agora, habilite novamente o pré-autenticação no portal de saudação e autenticar por meio do Azure, na tentativa de aplicativo de toohello tooconnect por meio de sua URL externa. Se tiver falhado SSO, você verá uma mensagem de erro proibido no navegador hello, além de evento 13022 no log de saudação:

    *Conector de Proxy de aplicativo Microsoft AAD não pode autenticar o usuário Olá porque o servidor de back-end Olá responde tooKerberos tentativas de autenticação com um erro HTTP 401.*

    ![Erro proibido HTTTP 401](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Verifique o pool de aplicativos do hello IIS aplicativo tooensure Olá configurado é configurado toouse Olá mesma conta Olá SPN foi configurada no AD, navegando no IIS conforme ilustrado abaixo

    ![Janela de configuração de aplicativo IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Depois que você sabe a identidade hello, emita o seguinte de saudação de um toomake de prompt de cmd se que essa conta definitivamente está configurada com hello SPN em questão. Por exemplo, **setspn – q http/spn.wacketywack.com**

    ![Janela de comando SetSPN](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Verifique que Olá SPN definido nas configurações do aplicativo hello no portal de saudação é Olá mesmo SPN configurado na conta de destino AD Olá em uso por pool de aplicativos do aplicativo hello

   ![Configuração de SPN no portal do Azure](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Vá para o IIS e selecione Olá **Editor de configuração** opção para o aplicativo hello e navegue muito**system.webServer/security/authentication/windowsAuthentication** toomake-se de que **UseAppPoolCredentials** é definido tootrue

   ![Opção de credencial de pools de aplicativo da configuração do IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Enquanto estiver sendo útil para melhorar o desempenho de saudação de operações do Kerberos, sair do modo de Kernel habilitado também faz com que o tíquete Olá para hello solicitado toobe serviço descriptografado usando a conta do computador. Isso também é chamado de sistema Local do hello, então ter quebra de tootrue este conjunto KCD quando o aplicativo hello está hospedado em vários servidores em um farm.

-   Como uma verificação adicional, você também pode desejar Olá toodisable **estendida** proteção muito. Foram encontrados cenários onde isso mostrou toobreak KCD quando habilitado em configurações muito específicas, em que um aplicativo é publicado como uma subpasta do site da Web padrão de saudação. Esse em si está configurado para autenticação anônima, deixando as caixas de diálogo todo Olá acinzentadas sugerindo objetos filho não seriam herdar as configurações ativas. Mas, onde possível sempre recomendamos com esta configuração habilitada, portanto por todos os de forma de teste, mas não se esqueça de toorestore este tooenabled.

Essas verificações adicionais devem ter colocá-lo no toostart de rastrear usando o aplicativo publicado. Você pode ir em frente e aceleração conectores adicionais também serão configurado toodelegate, mas se houver nenhuma outra seria sugerimos uma leitura de nosso passo a passo técnica mais detalhada [guia completo de saudação para aplicativo do AD do Azure de solução de problemas Proxy](https://aka.ms/proxytshootpaper)

Se você ainda não é possível tooprogress seu problema, suporte deve ser maior que tooassist feliz e continuar aqui. Crie um tíquete de suporte diretamente no portal de saudação e tentará alcançar nossos engenheiros tooyou.

## <a name="other-scenarios"></a>Outros cenários

-   Proxy de aplicativo do Azure solicita um tíquete Kerberos antes de enviar seu aplicativo tooan de solicitação. Alguns aplicativos de terceiros 3º como Tableau servidor não deseja que esse método de autenticação e em vez disso, espera hello mais convencional negociações tootake lugar. Olá primeira solicitação é anônima, permitindo Olá aplicativo toorespond com tipos de autenticação de saudação que ele oferece suporte a um 401.

-   Autenticação com salto duplo – comumente usado em cenários nos quais um aplicativo é hierárquico, com um back-end e front-end, ambos exigindo autenticação, como o Serviços de Relatórios SQL.

## <a name="next-steps"></a>Próximas etapas
[Configurar a KCD (delegação Restrita de Kerberos) em um domínio gerenciado](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
