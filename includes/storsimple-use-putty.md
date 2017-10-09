<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect por meio do console serial Olá
1. Conecte o dispositivo de toohello de cabo serial (diretamente ou através de um adaptador serial USB).
2. Olá abrir **painel de controle**e, em seguida, abra Olá **Gerenciador de dispositivos**.
3. Identifique a porta de saudação COM conforme mostrado na ilustração a seguir de saudação.
   
     ![Conectando por meio do console serial](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Inicie o PuTTY. 
5. No painel direito da saudação, alterar Olá **o tipo de Conexão** muito**Serial**.
6. No painel direito da saudação, digite a porta COM apropriada de saudação. Certifique-se de que os parâmetros de configuração serial Olá são definidos da seguinte maneira:
   
   * Velocidade: 115.200
   * Bits de dados: 8
   * Bits de parada: 1
   * Paridade: nenhuma
   * Controle de fluxo: nenhum
     
     Essas configurações são mostradas na ilustração a seguir de saudação.
     
     ![Configurações do PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Se saudação padrão controle de fluxo não funcionar, tente configurar o controle de fluxo da saudação tooXON/XOFF.
     > 
     > 
7. Clique em **abrir** toostart uma sessão serial.

