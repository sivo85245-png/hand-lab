# Hand + Face Lab — mãos e rosto

Protótipo separado da APS. Abra index.html no Chrome ou Edge com internet e clique
em Ativar câmera. Autorize a webcam no aviso do navegador. Microfone não é solicitado.

Se o navegador impedir o uso pelo arquivo, execute `python servidor.py` com Python
3.10 ou superior; isso serve a página em localhost. Não requer pacotes Python.

O sistema detecta até duas mãos, desenha 21 pontos em cada uma, mostra a lateralidade,
estima os dedos estendidos e identifica uma pinça por proximidade do polegar e indicador.
Não são sensores físicos: o modelo estima posições a partir das imagens.

A estimativa de dedos e de pinça usa regras geométricas simples. Rotação da mão,
oclusão e iluminação podem causar erros. Não serve para medidas clínicas ou de precisão.

O vídeo é processado no navegador e não é gravado nem enviado por este aplicativo.
Internet é usada para carregar MediaPipe 0.10.14, WebAssembly e modelo de detecção
a partir do jsDelivr e do armazenamento de modelos do Google. Esses serviços recebem
as requisições de download, mas este código não envia quadros da câmera a eles.

Desligar encerra as trilhas da webcam. Ocultar ou fechar a página também desliga.
Se houver erro de permissão, câmera ausente ou ocupada, a interface explica a causa.

Validação: sintaxe JavaScript verificada. Não foi realizado teste com webcam real;
precisão, desempenho e acesso à câmera precisam ser conferidos no dispositivo.

Documentação oficial:
https://developers.google.com/edge/mediapipe/solutions/vision/hand_landmarker/web_js


## Atualização: rastreamento facial

A mesma webcam agora processa até duas mãos e um rosto. Face Landmarker desenha
os pontos e a malha do rosto, olhos, íris, sobrancelhas, boca e contorno facial.
Os seletores permitem desligar mãos, rosto ou apenas a malha completa.

A abertura da boca é um coeficiente estimado do modelo, exibido de 0 a 100%; não é
medida física nem probabilidade de uma emoção. O indicador de olhos compara os
coeficientes eyeBlinkLeft e eyeBlinkRight com um limiar de 0,55. Pode falhar com
óculos, oclusão, iluminação ruim ou quando o rosto está virado.

Não há reconhecimento de identidade, inferência de emoções, gravação ou envio dos
quadros pelo aplicativo. Um modelo facial adicional é baixado do armazenamento
oficial do Google. O processamento conjunto pode reduzir a fluidez em computadores
menos potentes; desative um rastreamento se necessário.

Validação da atualização: sintaxe JavaScript e testes com dados simulados passaram
para malha facial, indicadores, ausência de rosto e desligamento das trilhas da
câmera. Ainda não foi testado com uma webcam real.

Referência: https://developers.google.com/edge/mediapipe/solutions/vision/face_landmarker/web_js
