toocreate uma rede virtual no modelo de implantação do Gerenciador de recursos hello usando Olá portal do Azure, siga as etapas de saudação abaixo. Saudação de uso [valores de exemplo](#values) se você estiver usando estas etapas como um tutorial. Se você não estiver fazendo o seguinte como um tutorial, ser valores de saudação tooreplace-se com seus próprios. Para obter mais informações sobre como trabalhar com redes virtuais, consulte Olá [visão geral da rede Virtual](../articles/virtual-network/virtual-networks-overview.md).

1. Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.
2. Clique em **Novo**. Em Olá **marketplace de saudação pesquisa** , digite 'Rede Virtual'. Localize **rede Virtual** de saudação retornada lista e clique em Olá tooopen **rede Virtual** folha.
3. Inferior Olá da folha de rede Virtual de saudação do hello **selecionar um modelo de implantação** , selecione **Gerenciador de recursos de**e, em seguida, clique em **criar**. Isso abre a folha de 'Criar rede virtual' hello.

    ![Folha Criar rede virtual](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Folha Criar rede virtual")
4. Em Olá **criar rede virtual** folha, definir configurações de rede virtual hello. Ao preencher os campos hello, hello de exclamação vermelho se torna uma marca de seleção verde quando caracteres hello inseridos no campo de saudação são válidos.

  - **Nome**: digite Olá nome para sua rede virtual. Neste exemplo, usamos TestVNet1.
  - **Espaço de endereço**: insira o espaço de endereço de saudação. Se você tiver várias tooadd de espaços de endereço, adicione o primeiro espaço de endereço. Você pode adicionar espaços de endereço adicionais mais tarde, depois de criar hello VNet. Verifique se esse espaço de endereço de saudação que você especificar não se sobrepõe ao espaço de endereço Olá para sua localização no local.
  - **Nome da sub-rede**: Adicionar Olá primeiro nome e a sub-rede endereço intervalo de sub-rede. Você pode adicionar sub-redes adicionais e a sub-rede de gateway hello mais tarde, depois de criar essa rede virtual. 
  - **Assinatura**: Verifique se que a assinatura Olá listada é Olá correto. Você pode alterar as assinaturas usando Olá lista suspensa.
  - **Grupo de recursos**: selecione um grupo de recursos existente ou crie um novo digitando um nome para seu novo grupo de recursos. Se você estiver criando um novo grupo, o grupo de recursos do nome hello tooyour de acordo com planejada valores de configuração. Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Local**: selecione Olá local para sua rede virtual. local de saudação determina onde recursos Olá que você implante toothis VNet residirá.

5. Selecione **Pin toodashboard** se desejar toofind capaz de toobe sua VNet facilmente no painel de saudação e, em seguida, clique em **criar**. Depois de clicar em **criar**, você verá um bloco no seu painel que refletirá o progresso de saudação da sua rede virtual. as alterações bloco Olá Olá rede virtual está sendo criado.
