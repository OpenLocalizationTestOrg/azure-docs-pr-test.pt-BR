As organizações vêm utilizando mais aplicativos de [SaaS (Software como serviço)](https://azure.microsoft.com/overview/what-is-saas/) para produtividade, uma vez que a tecnologia e as ferramentas de nuvem estão se tornando mais amplamente disponíveis. À medida que aumenta de número de saudação de aplicativos SaaS, torna-se um desafio para contas de toomanage administradores hello e direitos de acesso e para Olá usuários tooremember suas senhas diferentes. Gerenciar esses aplicativos individualmente cria mais trabalho e é menos seguro.

* Funcionários que têm tookeep controlar muitas senhas tendem toouse menos seguras métodos tooremembê-los a gravar senhas ou usando Olá mesmas senhas em várias contas.
* Quando chega um novo funcionário ou um funcionário deixa a organização, todas as suas contas devem ser provisionadas ou desconfiguradas individualmente.
* Além disso, a funcionários podem começar a usar aplicativos SaaS para o trabalho sem passar pela equipe de TI, que significa que eles estão criando suas próprias contas em sistemas que Olá os administradores de TI ainda não aprovado e não são de monitoramento.  

Uma solução para todos esses desafios é o SSO (logon único). Ele tem Olá toomanage de maneira mais simples com vários aplicativos e fornecer aos usuários uma experiência consistente de logon. Azure Active Directory (AD do Azure) fornece uma solução SSO robusta e tem muitos aplicativos pré-integrados disponíveis, com os tutoriais para que os administradores tooquickly configurar um novo aplicativo e iniciar o provisionamento de usuários.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Como o Active Directory do Azure integra aplicativos?
O AD do Azure permite que você toointegrate seus aplicativos e o provisionamento de contas. Isso pode ser feito por meio de uma de duas abordagens.

* Se o aplicativo hello previamente é integrado no aplicativo hello galeria, pode passar por esse portal tooset a aplicativos e configurar Olá configurações tooallow SSO. Para qualquer aplicativo da galeria, você pode começar, siga Olá simples instruções passo a passo apresentadas na Galeria de aplicativo hello e em Olá tooenable portal do Azure-logon único.
* Se aplicativo hello não estiver na Galeria de saudação, você ainda pode configurar o a maioria dos aplicativos no AD do Azure como um aplicativo personalizado. Isso exige um pouco mais técnica tooconfigure de Conhecimento. Você pode adicionar qualquer aplicativo que ofereça suporte ao SAML 2.0 como um aplicativo federado ou qualquer aplicativo que tenha uma página de entrada baseada em HTML como um aplicativo do SSO de senha.

Olá caso em que foram criadas pelos usuários suas próprias contas para aplicativos SaaS que não são gerenciados pelo IT, Olá [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) ferramenta fornece uma solução. Essa ferramenta monitora Olá web tráfego tooidentify quais aplicativos estão sendo usados em toda a organização hello e número de saudação de pessoas usando cada um deles. IT pode usar esse toolearn informações que os usuários Olá de aplicativos preferem e decidir quais toointegrate no AD do Azure para SSO.  

Ao integrar um aplicativo no AD do Azure, você pode mapear identidades do usuários Olá aplicativo estabelecida identidades tootheir respectivo AD do Azure.  

