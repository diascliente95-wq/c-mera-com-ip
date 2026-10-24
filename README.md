# IP Cam Connect

Projeto web para transmitir a câmera de um celular para outro aparelho pela internet, usando WebRTC e PeerJS.

## Páginas
- `index.html`: painel principal e conexão com câmeras IP que oferecem streams compatíveis.
- `camera.html`: ativa a câmera deste celular, com permissão explícita, e envia vídeo ao visualizador autorizado.
- `viewer.html`: gera um código temporário para receber o vídeo.

## Publicar pelo GitHub Pages
1. Abra **Settings → Pages** no repositório.
2. Escolha **Deploy from a branch**, selecione `main` e `/(root)`, depois salve.
3. Aguarde a publicação. As páginas ficarão disponíveis em `/camera.html` e `/viewer.html` no mesmo domínio.

## Como usar entre dois celulares
1. Publique o site e abra-o nos dois aparelhos usando HTTPS.
2. No celular que vai receber o vídeo, abra `viewer.html` e aguarde aparecer o código temporário.
3. Copie esse código e envie em privado para a pessoa que está com o celular transmissor.
4. No celular que vai transmitir, abra `camera.html`, toque **Ativar câmera e gerar código** e autorize a câmera.
5. Cole o código do visualizador no campo **Código do visualizador autorizado** e toque **Conectar e transmitir**.
6. No fim, toque **Parar transmissão**. O visualizador pode também desconectar.

## Segurança e limitações
- O vídeo só começa após ação visível para ativar a câmera e conceder permissão. O navegador exibe indicadores de câmera; mantenha a página aberta.
- O transmissor inicia a chamada para o código de visualizador fornecido, reduzindo chamadas não solicitadas. Compartilhe o código de visualização apenas com a pessoa autorizada.
- PeerJS Cloud é usado como serviço de sinalização. A mídia usa WebRTC criptografado e normalmente vai diretamente entre os aparelhos; o serviço de sinalização não é um sistema de contas ou autenticação. Para uso sensível/produção, recomenda-se um PeerServer próprio, autenticação e TURN controlado por você.
- A conexão pode falhar em algumas operadoras móveis ou redes com NAT restritivo. Nesse caso, é necessário configurar um servidor TURN confiável com credenciais temporárias. Não há garantia de conexão em toda rede móvel.
- A câmera do navegador requer HTTPS ou contexto seguro, permissão explícita e página aberta. Funcionamento em segundo plano não é garantido por navegadores móveis.
- Ambos os aparelhos precisam de internet. Não é preciso expor uma porta de câmera residencial nem usar o IP local do celular.
- Este protótipo não grava nem armazena vídeo. Use somente dispositivos e ambientes para os quais você tem autorização.
- A biblioteca PeerJS é carregada de CDN; se a biblioteca ou o serviço de sinalização estiver indisponível, a conexão não iniciará.

## Referências técnicas
- [PeerJS — início rápido](https://peerjs.com/client/getting-started)
- [PeerJS — FAQ e TURN](https://peerjs.com/client/faq)
- [PeerJS — API de Peer](https://peerjs.com/client/api/peer)
