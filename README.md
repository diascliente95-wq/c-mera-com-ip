# IP Cam Connect

Painel web responsivo para visualizar streams de câmeras IP autorizadas.

## Recursos iniciais
- Conexão por URL HTTP/HTTPS compatível com o navegador.
- Modos para MJPEG, HLS e imagem estática.
- Lista local de câmeras salvas no navegador.
- Tela cheia e mensagens de status.

## Limitações importantes
- Isso é uma interface web, não um aplicativo Android nativo.
- IP local (ex.: 192.168.x.x) normalmente só funciona dentro da mesma rede ou por VPN.
- Acesso remoto exige configuração no roteador, VPN ou serviço seguro do fabricante; prefira VPN e evite expor a câmera diretamente à internet.
- RTSP não é reproduzido diretamente pela maioria dos navegadores. Para RTSP, configure um gateway que converta para WebRTC/HLS.
- HTTPS pode bloquear URLs de vídeo HTTP por conteúdo misto. O fluxo também precisa permitir acesso do navegador e, quando aplicável, CORS.
- A página não descobre IPs nem tenta contornar login ou permissões. Use apenas câmeras que você administra ou tem autorização para acessar.

## Publicar pelo GitHub Pages
1. Abra Settings no repositório.
2. Em Pages, escolha Deploy from a branch.
3. Selecione `main` e `/ (root)`, depois Save.
4. Aguarde a publicação e abra o endereço indicado pelo GitHub Pages.

Para converter em aplicativo Android, uma etapa futura pode empacotar o site em uma aplicação nativa/PWA, mas o suporte a streams dependerá da câmera e da rede.
