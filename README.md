# IP Cam Connect

Projeto web para transmitir a câmera de um celular para outro aparelho pela internet, usando WebRTC e PeerJS.

## Páginas
- `index.html`: painel principal e conexão com câmeras IP que oferecem streams compatíveis.
- `camera.html`: transforma este celular em transmissor de câmera, mediante permissão explícita.
- `viewer.html`: visualiza o fluxo usando o código temporário do transmissor.

## Publicar pelo GitHub Pages
1. Abra **Settings → Pages** no repositório.
2. Escolha **Deploy from a branch**, selecione `main` e `/(root)`, depois salve.
3. Aguarde a publicação. As páginas ficarão disponíveis em `/camera.html` e `/viewer.html` no mesmo domínio.

## Como usar
1. Publique o site e abra-o em ambos os celulares por HTTPS.
2. No celular que vai funcionar como câmera, abra `camera.html`, toque **Ativar câmera e gerar código** e permita o acesso solicitado pelo navegador.
3. Envie o código temporário em privado para o outro aparelho.
4. No segundo celular, abra `viewer.html`, informe o código e toque **Conectar e assistir**.
5. Para terminar, toque **Parar transmissão** no aparelho transmissor e **Desconectar** no visualizador.

## Segurança e limitações
- O vídeo só começa após uma ação visível do usuário para ativar a câmera e conceder permissão. O navegador exibe os indicadores de câmera; mantenha a página aberta.
- O código do PeerJS é temporário e deve ser compartilhado apenas com pessoas autorizadas. Não publique o código.
- PeerJS Cloud é usado como serviço de sinalização. A mídia usa WebRTC criptografado e normalmente vai diretamente entre os aparelhos; o serviço de sinalização não é um sistema de contas ou autenticação. Para uso sensível/produção, recomenda-se um PeerServer próprio, autenticação e TURN controlado por você.
- A conexão pode falhar em algumas operadoras móveis ou redes com NAT restritivo. Nesse caso, é necessário configurar um servidor TURN confiável com credenciais temporárias. Não há garantia de conexão em toda rede móvel.
- A câmera do navegador requer HTTPS ou contexto seguro, permissão explícita e página aberta. O funcionamento em segundo plano não é garantido por navegadores móveis.
- O acesso remoto exige internet nos dois aparelhos. Não é preciso expor uma porta de câmera residencial nem usar o IP local do celular.
- Não há gravação nem armazenamento de vídeo neste protótipo. Use somente dispositivos e ambientes para os quais você tem autorização.
- A biblioteca PeerJS é carregada de CDN; se a biblioteca ou o serviço de sinalização estiver indisponível, a conexão não iniciará.

## Referências técnicas
- [PeerJS — início rápido](https://peerjs.com/client/getting-started)
- [PeerJS — FAQ e TURN](https://peerjs.com/client/faq)
- [PeerJS — API de Peer](https://peerjs.com/client/api/peer)
