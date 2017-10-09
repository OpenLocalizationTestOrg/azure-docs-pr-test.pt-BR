# <a name="securing-docker-containers-in-azure-container-service"></a>Protegendo os contêineres do Docker no Serviço de Contêiner do Azure

Este artigo apresenta as considerações e as recomendações para proteger os contêineres do Docker implantados no Serviço de Contêiner do Azure. Muitas dessas considerações se aplicam geralmente contêineres tooDocker implantados no Azure ou em outros ambientes. 

## <a name="image-security"></a>Segurança da imagem

Os contêineres são criados a partir de imagens que são armazenadas em um ou mais repositórios. Esses repositórios podem pertencer toopublic ou registros de contêiner privado. Um exemplo de um registro público é o [Docker Hub](https://hub.docker.com/). Um exemplo de um registro particular é hello [registro confiável do Docker](https://docs.docker.com/datacenter/dtr/2.0/), que pode ser instalado localmente ou em uma nuvem privada virtual. Há também serviços de registro de contêiner privado baseados em nuvem incluindo [Registro de Contêiner do Azure](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Imagens públicas e privadas
Em geral, assim como acontece com qualquer pacote de software publicado publicamente, uma imagem de contêiner disponível publicamente não garante a segurança. As imagens de contêiner são compostas por várias camadas de software e cada camada de software pode ter vulnerabilidades. Seja toounderstand chave Olá origem da imagem de contêiner hello, incluindo Olá proprietário da imagem da saudação (toodetermine se é uma fonte confiável ou não), Olá camadas de software consiste em e Olá versões de software. 

Por exemplo, se você for toohello oficial [nginx repositório](https://hub.docker.com/_/nginx/) no Hub do Docker e navegue toohello **marcas** guia, consulte vulnerabilidades codificado por cores em cada imagem. Cada cor representa vulnerabilidade de saudação de uma camada de software de imagem de saudação. Para saber mais sobre a verificação de vulnerabilidades no Docker Hub, veja [Noções básicas sobre repositórios oficiais no Docker Hub](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/).

![Imagens de nginx no Docker Hub](./media/container-service-security/docker-hub-nginx.png)

As empresas muito cuidado sobre segurança e tooprotect-se contra ataques de segurança devem armazenar e recuperar imagens de um registro particular, como o registro de contêiner do Azure ou registro confiável do Docker. Em adição tooproviding um registro particular gerenciado, registro de contêiner do Azure suporta [autenticação baseada em entidade de serviço](../articles/container-registry/container-registry-authentication.md) por meio do Active Directory do Azure para fluxos de autenticação básica, incluindo o acesso baseado em função para somente leitura, gravação e permissões de proprietário.

### <a name="image-security-scanning"></a>Verificação de segurança de imagem

Mesmo ao usar um registro particular, é uma imagem de toouse boa ideia verificar soluções para validação de segurança adicional. Cada camada de software em uma imagem de contêiner é potencialmente propensas toovulnerabilities independente de outras camadas na imagem de contêiner de saudação. Como cada vez mais empresas começar a implantar suas cargas de trabalho de produção com base nas tecnologias de contêiner, varredura de imagem se torna importante tooensure prevenção de ameaças de segurança em suas organizações. 

Monitoramento e verificação de soluções, como segurança [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) e [Aqua segurança](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), entre outros, pode ser usado tooscan imagens de contêiner em um registro particular e identificar vulnerabilidades potenciais. É importante fornecer toounderstand profundidade de saudação de verificação que Olá diferentes soluções. Por exemplo, algumas soluções podem apenas realizar a verificação cruzada entre as camadas de imagem em relação a vulnerabilidades conhecidas. Essas soluções podem não ser capaz de tooverify software de camada de imagem criado por meio de determinados software do Gerenciador de pacote. Outras soluções têm integração de verificação mais profunda e podem encontrar vulnerabilidades em qualquer software de pacote.

### <a name="production-deployment-rules-and-audit"></a>Regras de implantação de produção e auditoria
Quando um aplicativo é implantado na produção, é essencial tooset alguns tooensure de regras que as imagens usadas em ambientes de produção são seguras e não conter nenhuma vulnerabilidades.

* Como regra, não imagens com vulnerabilidades, ainda menores, devem ser permitidas toorun em um ambiente de produção. Além disso, todas as imagens de implantação em produção devem idealmente ser salvo em um registro privada, selecione tooa acessível apenas alguns. Também é número de saudação tookeep importante de produção imagens pequenas tooensure, que podem ser gerenciadas com eficiência.

* Desde que seja toopinpoint rígido Olá origem do software usando uma imagem de contêiner disponível publicamente, é imagens de toobuild uma boa prática de Conhecimento de tooensure de origem de origem de saudação da camada de saudação. Quando um superfícies de vulnerabilidade de uma imagem de contêiner automática interna, os clientes poderão encontrar uma resolução mais rápida de tooa de caminho. Com uma imagem pública, os clientes precisariam toofind raiz de saudação de uma imagem pública toofix-lo ou obter outra imagem segura de publicador hello.

* Uma imagem digitalizada totalmente implantada na produção não é garantida toobe backup toodate para tempo de vida de saudação do aplicativo hello. Vulnerabilidades de segurança podem ser relatadas para camadas de imagem de saudação que não eram anteriormente conhecidas ou introduzidas após a implantação de produção de hello. Auditoria periódica de imagens de implantação na produção é imagens tooidentify necessárias que estão desatualizados ou não foram atualizadas dentro de alguns instantes. Você pode usar metodologias de implantação de verde e azul e implantar imagens de contêiner tooupdate mecanismos de atualização sem tempo de inatividade. Verificação de imagem pode ser feito com ferramentas descritas Olá anterior da seção. 

* Um pipeline de CI (integração contínua) verificação de segurança integrada e imagens toobuild podem ajudar a manter registros privados seguros com imagens seguras de contêiner. Olá verificação de vulnerabilidade incorporados a solução de CI Olá garante imagens que passarem em todos os testes de saudação são enviados por push toohello registro privada implantadas de quais produção cargas de trabalho. Uma falha de pipeline CI garante que vulnerável imagens não são inseridas no registro privada hello, usado para implantações de carga de trabalho de produção. Isso também automatiza a verificação de segurança de imagem se houver um número significativo de imagens. Caso contrário, a auditoria manual de imagens em busca de vulnerabilidades de segurança pode ser muito demorada e sujeita a erros.

## <a name="host-level-container-isolation"></a>Isolamento de contêiner de nível de host
Quando um cliente implanta aplicativos de contêiner nos recursos do Azure, eles são implantados em um nível de assinatura em grupos de recursos e não são multilocatários. Isso significa que se um cliente compartilha uma assinatura com outras pessoas, não há nenhum limites que podem ser criados entre duas implantações em Olá mesmo assinatura. Portanto, a segurança de nível de contêiner não estará garantida. 

Também é toounderstand crítico que contêineres compartilham kernel hello e recursos de saudação do host de saudação (que, no serviço de contêiner do Azure, é uma VM do Azure em um cluster). Portanto, os contêineres em produção devem ser executados no modo de usuário sem privilégios. Executando um contêiner com privilégios de raiz pode comprometer a todo o ambiente de saudação. Com acesso de nível raiz em um contêiner, um hacker pode acessar toohello privilégios de raiz totais no host de saudação. Além disso, é importante toorun contêineres com sistemas de arquivos somente leitura. Isso impede que alguém que tenha acesso toohello comprometido contêiner toowrite scripts mal-intencionados toohello sistema de arquivos e acessar arquivos tooother. Da mesma forma, é importante toolimit Olá os recursos (como memória, CPU e largura de banda de rede) alocados tooa contêiner. Isso ajuda a impedir que hackers precisam de mais recursos e buscando atividades ilegais como fraude de cartão de crédito ou de mineração bitcoin, que pode impedir que outros contêineres em execução no cluster ou host hello.

## <a name="orchestrator-considerations"></a>Considerações sobre o Orchestrator

Cada orquestrador disponível no Serviço de Contêiner do Azure tem suas próprias considerações de segurança. Por exemplo, você deve limitar direto nós tooorchestrator de acesso SSH no serviço de contêiner. Em vez disso, você deve usar a interface do usuário de cada orchestrator ou ferramentas de linha de comando (como `kubectl` para Kubernetes) toomanage ambiente de contêiner Olá sem acessar Olá hosts. Para obter mais informações, consulte [criar um cluster de conexão remota tooa Kubernetes, o controlador de domínio/sistema operacional ou o Docker Swarm](../articles/container-service/kubernetes/container-service-connect.md).

Para obter informações adicionais de segurança específicas do orchestrator, consulte Olá recursos a seguir:

* **Kubernetes**: [práticas recomendadas de segurança para implantação de Kubernetes](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [proteção do cluster](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [segurança do Docker](https://www.docker.com/docker-security)

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre a segurança de arquitetura e o contêiner do Docker, consulte [tooContainer Introdução segurança](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Para obter informações sobre a segurança da plataforma Windows Azure, consulte Olá [Central de segurança do Azure](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
