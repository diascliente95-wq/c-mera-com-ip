# IP Cam Connect

Projeto web para câmeras IP e transmissão de vídeo entre celulares autorizados.

## Páginas
- `index.html`: painel principal para streams HTTP/HTTPS compatíveis (MJPEG/HLS/imagem).
- `camera.html`: ativa a câmera deste celular com permissão explícita e envia vídeo ao visualizador via WebRTC/PeerJS.
- `viewer.html`: gera um código temporário para receber vídeo do transmissor.
- `acesso-ip.html`: analisa sintaticamente um IPv4 e explica limitações do acesso remoto.
- `conectar.html`: login Firebase, cadastro por nome e protótipo de chamada WebRTC entre aparelhos da mesma conta.
- `firebase-config.js`: modelo para configurar o app Web do Firebase.
- `firestore.rules`: regras iniciais para limitar dados à conta autenticada.

## Publicar pelo GitHub Pages
1. Abra **Settings → Pages** no repositório.
2. Escolha **Deploy from a branch**, selecione `main` e `/(root)`, depois salve.
3. Aguarde a publicação. As páginas estarão no mesmo endereço do site, em `/camera.html`, `/viewer.html` e `/acesso-ip.html`.

## Como usar o protótipo WebRTC
1. Abra `viewer.html` no aparelho que vai assistir e copie o código temporário gerado.
2. No transmissor, abra `camera.html`, toque para ativar a câmera e conceda permissão.
3. Cole o código do visualizador e toque em **Conectar e transmitir**.
4. Encerre a transmissão no aparelho transmissor quando terminar.

## Sobre “digitar somente o IP” através da internet móvel
O protótipo atual **não permite** ligar um celular remoto somente digitando o IP público. Não afirmamos que isso funcione, porque:
- O IP local (por exemplo, `192.168.x.x`) só é roteável na rede local ou numa VPN conectada.
- Muitas operadoras móveis usam CGNAT e firewalls, que bloqueiam conexões de entrada para o aparelho.
- Uma página web no celular não abre uma porta TCP/UDP para atuar como servidor de vídeo. A câmera web atual envia mídia por WebRTC, que usa sinalização para estabelecer a sessão.
- Mesmo um IP público não basta sem um endpoint de vídeo ativo, porta roteável e regras de firewall adequadas.

### Arquitetura viável
**Opção A — mais prática em redes móveis:** manter WebRTC, adicionar contas/autenticação e pareamento por nome de dispositivo, além de um serviço de sinalização próprio e um servidor TURN confiável com credenciais temporárias. O usuário poderá selecionar um dispositivo pareado sem digitar códigos em cada conexão. TURN retransmite mídia quando a conexão direta falha e pode gerar custos de banda.

**Opção B — IP como destino:** instalar um aplicativo Android nativo que atue como serviço de transmissão, com autenticação, e conectar os dois celulares por uma VPN privada com IPs estáveis. O visualizador usa o IP VPN do transmissor. Um IP público direto só é uma alternativa se a rede fornecer endereço roteável e permitir a porta necessária; não é garantido por operadoras móveis.

O arquivo `acesso-ip.html` é um diagnóstico local de formato/faixas de IP; não testa acessibilidade real e não transmite vídeo. Para dispensar códigos manuais com segurança, a próxima etapa recomendada é autenticação e pareamento de dispositivos, não usar um IP público como identidade.

## Segurança e limitações
- Câmera inicia apenas após ação visível e permissão do usuário; mantenha a página aberta. Navegadores móveis não garantem execução em segundo plano.
- PeerJS Cloud é usado como sinalização no protótipo atual; não é autenticação de usuários. Para uso sensível/produção, implemente contas, autorização, servidor de sinalização próprio e TURN controlado por você.
- WebRTC usa mídia criptografada, mas conectividade depende de ICE/STUN/TURN, firewall, NAT e qualidade da rede. Algumas operadoras podem não conectar sem TURN.
- Não grava nem armazena vídeo. Use apenas aparelhos e ambientes para os quais você tem autorização.
- O projeto carrega a biblioteca PeerJS por CDN; sem acesso à biblioteca ou ao serviço de sinalização, a conexão não inicia.

## Referências
- [WebRTC protocols: ICE, STUN e TURN (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Protocols)
- [WebRTC — getting started with remote streams](https://webrtc.org/getting-started/remote-streams)
- [RFC 8828 — WebRTC IP Address Handling Requirements](https://www.rfc-editor.org/rfc/rfc8828.html)


## Configuração da conta e aparelhos

1. Crie um projeto no [Firebase Console](https://console.firebase.google.com/).
2. Adicione um aplicativo Web e copie a configuração para `firebase-config.js`. Não coloque senhas de servidor nesse arquivo.
3. Em **Authentication → Sign-in method**, ative **E-mail/Senha**.
4. Crie o banco **Cloud Firestore** e publique as regras de `firestore.rules` pela aba **Rules**.
5. Publique novamente o site pelo GitHub Pages e abra `conectar.html`.
6. Entre com a mesma conta nos dois celulares e registre cada um com um nome diferente.

**Importante:** `conectar.html` já inclui um fluxo inicial de chamada WebRTC por nome usando PeerJS para sinalização. Ainda é um protótipo: não foi testado em dois celulares reais, a configuração TURN não está incluída e certas redes móveis podem bloquear a conexão direta. Use regras restritas do Firestore e teste somente com aparelhos autorizados. Veja a documentação oficial sobre [segurança do Firestore](https://firebase.google.com/docs/firestore/security/overview).
