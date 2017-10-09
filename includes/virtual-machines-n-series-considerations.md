## <a name="deployment-considerations"></a>Considerações de implantação

* Para ver a disponibilidade das VMs da Série N, veja [Produtos disponíveis por região](https://azure.microsoft.com/en-us/regions/services/).

* As VMs da série N só podem ser implantadas no modelo de implantação do Gerenciador de recursos de saudação.

* Quando criar uma VM série N usando Olá portal do Azure, Olá **Noções básicas de** folha, selecione um **tipo de disco VM** de **HDD**. tamanho de toochoose uma série de N disponível, em Olá **tamanho** folha, clique em **exibir todos os**.

* As VMs da Série N não dão suporte a discos de VM incluídos em backup no armazenamento Premium do Azure.

* Se você quiser toodeploy mais do que alguns VMs da série de N, considere uma assinatura paga pelo uso ou outras opções de compra. Se estiver usando uma [conta gratuita do Azure](https://azure.microsoft.com/free/), você poderá usar apenas um número limitado de núcleos de computação do Azure.

* Você pode precisar de uma cota de núcleos de saudação tooincrease (por região) em sua assinatura do Azure e aumentar a cota de saudação separado para NC ou NV núcleos. aumentar a cota toorequest, [abrir uma solicitação de suporte do cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) sem custo adicional. Os limites padrão podem variar dependendo de sua categoria de assinatura.

* Uma imagem de VM, você pode implantar nas VMs da série N é hello [máquina de Virtual de ciência de dados do Azure](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Olá máquina de Virtual de ciência de dados pré-instala e configura muitos ciência de dados populares e profundo ferramentas de aprendizado. Ele também pré-instala drivers NVIDIA Tesla GPU para instâncias de NC.





