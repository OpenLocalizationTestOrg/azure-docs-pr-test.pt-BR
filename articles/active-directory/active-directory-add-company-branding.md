---
title: "marca tooyour entrar e páginas de painel de acesso da empresa de aaaAdd"
description: "Saiba como tooadd uma página toohello sign-in do Azure da identidade visual da empresa e hello acessam a página de painel"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Adicionar identidade visual tooyour entrar e páginas de painel de acesso da empresa
tooavoid confusão, muitas empresas deseja tooapply uma aparência consistente em todos os sites de saudação e serviços que gerenciam. O Azure Active Directory fornece esse recurso, permitindo-lhe toocustomize aparência de saudação do hello páginas da web com o logotipo da empresa e esquemas de cores personalizadas a seguir:

* **Na página de entrada** -isso é página Olá que aparece quando você entrar no tooOffice 365 ou outros aplicativos baseados na web que estão usando o AD do Azure como seu provedor de identidade. Você interage com esta página durante uma descoberta de Realm inicial ou tooenter suas credenciais. Olá Home Realm Discovery permite Olá sistema tooredirect federado usuários tootheir local STS (como o AD FS).
* **Página do painel de acesso** - Olá painel de acesso é um portal baseado na web que permite que você tooview e ative Olá baseado em nuvem aplicativos o administrador do AD do Azure concedeu a você acesso para. tooaccess Olá painel de acesso, use Olá URL a seguir: [https://myapps.microsoft.com](https://myapps.microsoft.com).

Este tópico explica como você pode personalizar a página de entrada hello e página de saudação do painel de acesso.

> [!NOTE]
> * Identidade visual da empresa é um recurso que está disponível somente se você atualizar toohello Premium ou edição Basic do Active Directory do Azure, ou for um usuário do Office 365. Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).
> * O Azure Active Directory Premium e edições Basic estão disponíveis para clientes na China usando a instância mundial de saudação do Active Directory do Azure. O Azure Active Directory Premium e edições Basic não têm suporte no momento no serviço do Microsoft Azure Olá operado pela 21Vianet na China. Para obter mais informações, entre em contato conosco em Olá [Fórum do Active Directory do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Personalizando a página de entrada hello
Normalmente, se você precisar de acesso baseado em navegador tooyour nuvem aplicativos e serviços que sua empresa assina, você usa página de entrada hello.

Se você aplicou alterações tooyour na página de entrada, pode levar a hora de tooan para Olá alterações tooappear.

Uma página de entrada com marca só aparece quando você visita um serviço com uma URL específica do locatário, como https://outlook.com/**contoso**.com ou https://mail.**contoso**.com.

Quando você visita um serviço com URLs específicas sem locatário (por exemplo, https://mail.office365.com), uma página de entrada sem marca é exibida. Nesse caso, sua identidade visual aparecerá assim que você inserir sua ID de usuário ou que tiver selecionado um bloco de usuário.

> [!NOTE]
> * O nome do domínio deve aparecer como "Ativo" no hello **do Active Directory** > **diretório** > **domínios** seção Olá portal clássico do Azure onde você configurou a identidade visual.
> * Identidade visual da página de entrada não reporta o sinal do consumidor toohello na página do Microsoft. Se você entrar com uma conta pessoal da Microsoft, você pode ver a lista marcada de blocos do usuário renderizados pelo AD do Azure, mas Olá identidade visual da sua organização não se aplica toohello página de logon da conta de Microsoft.
>
>

Se você quiser tooshow a marca da empresa, cores e outros elementos personalizáveis nesta página, consulte Olá diferença de saudação toounderstand imagens entre duas experiências de saudação a seguir.

Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **antes de** uma personalização:

![Página de entrada do Office 365 antes da personalização][1]

Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **depois** uma personalização:

![Página de entrada do Office 365 após a personalização][2]

Olá seguinte captura de tela mostra um exemplo de página de entrada hello Office 365 em um dispositivo móvel **antes de** uma personalização:

![Página de entrada do Office 365 antes da personalização][3]

Olá seguinte captura de tela mostra um exemplo de página de entrada hello Office 365 em um dispositivo móvel **depois** uma personalização:

![Página de entrada do Office 365 após a personalização][4]

Quando você redimensiona uma janela do navegador, Olá ilustração grande, como Olá mostrada anteriormente, geralmente é cortada tooaccommodate taxas de proporção de tela diferente. Com isso em mente, você deve tentar tookeep Olá principais elementos visuais na ilustração Olá para que eles sempre aparecem no canto superior esquerdo de saudação (superior direito para idiomas da direita para esquerda). Isso é importante porque o redimensionamento geralmente ocorre de contínuo do canto inferior direito Olá em direção à saudação superior / esquerdo ou da parte inferior da saudação em direção à parte superior da saudação.

Olá imagem a seguir mostra como ilustração de saudação é cortada quando o navegador de saudação é redimensionado toohello à esquerda:

![][6]

Aqui está como ela aparece depois Olá navegador é redimensionado em direção à parte superior da saudação:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Quais elementos na página Olá posso personalizar?
Você pode personalizar Olá elementos a seguir na página de entrada hello:

![][5]

| Elemento de página | Local na página de saudação |
|:--- | --- |
| Logotipo de faixa |Mostrado na saudação de superior direita da página de saudação. Substitui o site de destino Olá logotipo Olá que estão entrando toodisplays (por exemplo Office 365 ou Azure). |
| Ilustração grande/cor da tela de fundo |Mostrado à esquerda de saudação da página de saudação. Substitui o site de destino Olá imagem Olá que estão entrando toodisplays. Olá cor de plano de fundo pode ser mostrada no lugar de saudação ilustração grande em conexões de largura de banda baixa ou em telas estreitas. |
| Mantenha-me conectado |Mostrado na caixa de texto de senha hello. |
| Texto da página de entrada |Mostrado acima rodapé hello quando você precisar de informações úteis de tooconvey antes de uma entrada com uma conta corporativa ou escolar. Por exemplo, você talvez queira tooinclude Olá phone número tooyour técnico, ou uma instrução legal. |

> [!NOTE]
> Todos os elementos são opcionais. Por exemplo, se você especificar um logotipo de faixa, mas sem uma ilustração grande, página de entrada hello mostra a ilustração logotipo e Olá Olá para site de destino (ou seja, Olá Califórnia do Office 365 da estrada imagem).
>
>

Na página entrar, Olá **Mantenha-me conectado** caixa de seleção permite que um tooremain do usuário conectado ao fechar e reabrir o navegador. Ela não afeta o tempo de vida da sessão. Você pode ocultar Olá a caixa de seleção na página de entrada do Active Directory do Azure de saudação.

Se a caixa de seleção de saudação é exibida depende de configuração de saudação do **KMSI ocultar**.

![][9]

toohide Olá caixa de seleção, defina essa configuração muito**Hidden**.

> [!NOTE]
> Alguns recursos do SharePoint Online e o Office 2010 dependem usuários sendo capaz de toocheck nesta caixa. Se você configurar toohidden essa configuração, os usuários podem ver prompts adicionais e inesperados em toosign.
>
>

Você também pode localizar todos os elementos desta página. Depois de configurar um elemento “padrão” de personalização, você pode configurar mais versões para localidades diferentes. Você também pode misturar e combinar vários elementos. Por exemplo, você pode:

* Criar uma ilustração grande "padrão" que funciona para todas as culturas e depois criar versões específicas para o inglês e o francês. Quando você define sua tooone navegadores desses dois idiomas, imagem específica de saudação aparece, enquanto ilustração de padrão de saudação aparece para todos os outros idiomas.
* Configure logotipos diferentes para sua organização (por exemplo, versões em japonês ou hebraico).

## <a name="access-panel-page-customization"></a>Personalização da página Painel de Acesso
página de saudação do painel de acesso é essencialmente uma página do portal para aplicativos de nuvem toohello acesso rápido que tiver recebido acesso tooby seu administrador. Nessa página, seus aplicativos são exibidos como blocos de aplicativo clicáveis.

Olá captura de tela a seguir mostra um exemplo de uma página do painel de acesso após a personalização.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Configurar seu diretório com a identidade visual da empresa
Você pode configurar um conjunto padrão de elementos personalizáveis por diretório Olá portal clássico do Azure. Após terem sido salvas Olá padrões, um administrador pode adicionar versões localizadas de cada elemento para diferentes idiomas / localidades. Todos os elementos personalizáveis são opcionais.

Por exemplo, se você configurar um logotipo de faixa padrão, mas sem uma ilustração grande, página de entrada hello exibe seu logotipo no canto superior direito de saudação. No entanto ilustração de padrão de saudação do site de saudação é exibida.

Imagine Olá a seguinte configuração:

* Um logotipo de faixa padrão e um texto de página de entrada em inglês
* Um Texto de Página de entrada específico do idioma alemão

Se sua preferência de idioma alemão, você obtém saudação padrão logotipo do Banner mas Olá texto em alemão.

Enquanto você poderia configurar tecnicamente um conjunto diferente para cada idioma com suporte pelo AD do Azure, recomendamos que você mantenha muitas variações Olá baixas, por motivos de desempenho e manutenção.

> [!IMPORTANT]
> Yammer não não Olá Mostrar AD do Azure com a marca na página de entrada até depois Olá usuário faz logon. usuário Olá vê Olá página de entrada do Office 365 genérica primeiro e, em seguida, a saudação da marca página depois disso.   
 
 
**tooadd diretório de tooyour identidade visual da empresa, execute Olá etapas a seguir:**

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador do diretório Olá deseja toocustomize.
2. Selecione o diretório de saudação toocustomize desejado.
3. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurar**.
4. Clique em **Personalizar Identidade Visual**.
5. Modificar Olá elementos você deseja toocustomize. Todos os campos são opcionais.
6. Clique em **Salvar**.

Pode levar até horas tooan para nova alteração é feita toohello entrar identidade visual da página tooappear.

**empresa de idioma específico tooadd identidade visual, execute Olá etapas a seguir:**

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador do diretório Olá deseja toocustomize.
2. Selecione o diretório de saudação toocustomize desejado.
fs3. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurar**.
4. Clique em **Personalizar Identidade Visual**.
5. Clique em **Adicionar identidade visual para um idioma específico**.
6. Selecione Olá idioma você deseja o logotipo de saudação toocustomize para e, em seguida, clique em **próximo**.
7. Edite somente os elementos de saudação do qual você deseja substitui tooconfigure específico do idioma. Todos os campos são opcionais. Se um campo for deixado em branco, em seguida, valor padrão personalizado de saudação é exibida em vez disso (ou Olá padrão da Microsoft se um padrão personalizado não está configurado).
8. Clique em **Salvar**.

**marca do seu diretório da empresa tooremove execute Olá etapas a seguir:**

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador do diretório Olá deseja toocustomize.
2. Selecione o diretório de saudação toocustomize desejado.
3. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurar**.
4. Clique em **Personalizar Identidade Visual**.
5. Na página Personalizar identidade visual hello, selecione **editar configurações de identidade visual existentes** e, em seguida, vá toohello próxima página.
6. Dependendo de quais elementos você deseja tooremove, siga um ou mais dos seguintes hello:

    a. Em **Logotipo de Faixa**, selecione **Remover logotipo carregado**.

    b. Em **Logotipo de Bloco**, selecione **Remover logotipo carregado**.

    c. Remova o texto de saudação de todas as caixas de texto.

    d. Clique em **Avançar**.

    e. Remova o texto de saudação de todas as caixas de texto.
7. Clique em **salvar** tooremove elementos de saudação.
8. Se necessário, clique em **personalizar identidade visual** novamente e repita essas etapas para todos os idiomas identidade visual específica que precisa toobe removido.
    Todas as configurações de identidade visual foram removidas quando você clicar em **personalizar identidade visual** e consulte Olá **personalizar identidade visual padrão** formulário com sem configurações existentes.

## <a name="testing-and-examples"></a>Testes e exemplos
É recomendável que você experimente um locatário de teste antes de fazer alterações em seu ambiente de produção.

**tooverify se sua identidade visual foi aplicada:**

1. Abra uma sessão de navegador InPrivate ou Incognito.
2. Visite https://outlook.com/contoso.com, substituindo contoso.com pelo domínio Olá que você personalizou.

Isso também funciona com domínios que se parecem com contoso.onmicrosoft.com.

toohelp criar conjuntos de personalização eficientes, Personalizamos Olá dois fictícias páginas de entrada a seguir:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest configurações de idioma específico Olá, é necessário preferências de idioma do toomodify saudação padrão em seu idioma de tooa do navegador da web que você definiu na sua personalização. No Internet Explorer, você configurá-la no hello **opções da Internet** menu.

## <a name="customizable-elements"></a>Elementos personalizáveis
Alguns elementos personalizáveis no AD do Azure têm vários casos de uso. Você pode configurar uma vez por diretório logotipos da empresa e é usada em ambos Olá entrar e páginas de painel de acesso. Alguns elementos personalizáveis são específicos somente toohello na página de entrada. Olá tabela a seguir fornece detalhes para Olá diferentes elementos personalizáveis.

| Nome | Descrição | Restrições | Recomendações |
| --- | --- | --- | --- |
| Logotipo de faixa |Olá logotipo do Banner é exibido na página de entrada hello e painel de acesso de saudação. |<p>JPG ou PNG</p><p>60 x 280 pixels</p><p>10 KB</p> |<p>Use o logotipo completo da sua organização (incluindo pictograma e logotipo)</p><p>Mantenha-o em 30 pixels tooavoid alta introduzir barras de rolagem em dispositivos móveis</p><p>Mantenha-o com menos de 4 KB</p><p>Use um PNG transparente (não presuma que Olá na página de entrada sempre tem um plano de fundo branco)</p> |
| Logotipo de organização lado a lado |(atualmente não usado na página de entrada hello) Em Olá futuro, esse texto pode ser usado tooreplace Olá genérico "ou de estudante conta" símbolo em diferentes locais da experiência de saudação. |<p>JPG ou PNG</p><p>120 x 120 pixels</p><p>10 KB</p> |<p>Mantenha-o simples (sem texto pequeno), como essa imagem pode ser redimensionada too50% |
| </p> | | | |
| Rótulo de nome de usuário da página de entrada |(atualmente não usado na página de entrada hello) Em Olá futuro, esse texto pode ser usado tooreplace Olá genérico "ou de estudante conta" cadeia de caracteres em diferentes locais da experiência de saudação. Você pode definir toosomething como "Conta Contoso" ou "ID Contoso" |<p>Texto em Unicode, caracteres too50</p><p>Apenas texto sem formatação (sem links ou marcas HTML)</p> |<p>Mantenha-o curto e simples</p><p>Pergunte a seus usuários como eles geralmente consultam toohello trabalho ou conta de escola você os fornece.</p> |
| Texto da página de entrada |Esse texto "boilerplate" aparece abaixo do formulário de página de entrada hello e pode ser usado toocommunicate as instruções adicionais ou onde tooget ajuda e suporte. |<p>Texto em Unicode, caracteres too256</p><p>Apenas texto sem formatação (sem links ou marcas HTML)</p> |Mantenha abaixo de 250 caracteres (aproximadamente 3 linhas de texto) |
| Ilustração da página de entrada |Ilustração de saudação é uma imagem grande é exibida no Olá entrar página toohello à esquerda do formulário de página de entrada hello. |<p>JPG ou PNG</p><p>1.420 x 1.200</p><p>500 KB</p> |<p>1.420 x 1.200 pixels</p><p>Importante: mantenha o menor possível, idealmente abaixo de 200 KB. Se essa imagem for muito grande, o desempenho de saudação da página de entrada hello é afetado quando imagem Olá não é armazenado em cache</p><p>Esta imagem geralmente é cortada, tooaccommodate diferentes proporções de tela. Lembre-Olá canto superior esquerdo (canto superior direito para idiomas RTL), pois o redimensionamento ocorrerá do canto inferior/direito de hello, indo até Olá superior / esquerdo, como a janela do navegador Olá reduz elementos visuais primários de saudação.</p> |
| Cor da tela de fundo da página de entrada |cor de plano de fundo de página de entrada Hello é usado na esquerda de toohello área saudação do formulário de página de entrada hello. |Deve ser uma cor RGB em formato hexadecimal (exemplo: #FFFFFF) |<p>cor de plano de fundo Olá pode ser mostrada no lugar de saudação ilustração grande em conexões de baixa largura de banda</p><p>Sugerimos que você escolher a cor do principal de saudação do hello logotipo em faixa</p> |

## <a name="next-steps"></a>Próximas etapas
* [Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
