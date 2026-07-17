========================================================================
   PROJETO TESTE: AR.js (Marcadores Dinâmicos & QR Code Integration)
========================================================================

1. DESCRIÇÃO GERAL
------------------
Esta Prova de Conceito explora a biblioteca AR.js (Marker-based) configurada com 
uma arquitetura dinâmica via URL. Um único ficheiro 'index.html' consegue injetar 
modelos 3D e marcadores distintos dependendo dos parâmetros recebidos no link 
do QR Code, otimizando drasticamente a escalabilidade do projeto.

2. ESTRUTURA DE FICHEIROS
-------------------------
/ (Raiz do Projeto)
│
├── index.html               # Ficheiro com motor A-Frame + AR.js e Script Dinâmico
├── README.txt               # Documentação técnica do projeto
└── assets/
    ├── pattern-marker.patt  # Ficheiro do Marcador Personalizado (.patt)
    └── 02_Bolsos.glb        # Modelo 3D em formato GLTF/GLB

3. TECNOLOGIAS E DEPENDÊNCIAS
-----------------------------
- HTML5 / CSS3 / JavaScript (ES6 Vanilla)
- A-Frame v1.3.0
- AR.js v3.x (WebAR com suporte a Marcadores Pattern e Barcode 3x3 PARITY65)
- A-Frame Extras v6.1.1 (Para execução de animações)

4. ARQUITETURA E CORREÇÕES TÉCNICAS APLICADAS
---------------------------------------------
- Injeção Dinâmica via URL (URLSearchParams):
  * Exemplo Barcode: index.html?model=02_Bolsos&marker=2
  * Exemplo Pattern: index.html?model=02_Bolsos (Fallback automático para pattern-marker.patt)
- Correção do Feed de Vídeo / Zoom da Câmara (3 Combinações Aplicadas):
  1. Viewport Meta Tag: Impede o zoom digital e simulação desktop do browser móvel.
  2. CSS com `#arjs-video`: Forçado com `width: 100vw !important`, `height: 100vh !important` 
     e `object-fit: cover !important` para eliminar cortes e distorções.
  3. Resolução HD na Scene: Forçados os parâmetros 'sourceWidth: 1280; sourceHeight: 720; 
     displayWidth: 1280; displayHeight: 720;' no componente 'arjs'.
- Iluminação e Escala:
  * Renderizador configurado com `color-space="sRGB"` e `colorManagement: true`.
  * Modelo ajustado para `<a-gltf-model>` com a escala '15 15 15'.

5. COMO EXECUTAR
----------------
1. Servir o projeto num servidor Web com HTTPS ativo.
2. Testar o acesso através do browser móvel adicionando os parâmetros desejados na URL.

6. COMO TESTAR
--------------
- Teste com Marcador Personalizado:
  Acede a: 'https://teuservidor.com/index.html'
  Aponta a câmara para o marcador do bolso ou para o ficheiro 'pattern-marker.patt'.

- Teste com Código de Barras (Barcode):
  Acede a: 'https://teuservidor.com/index.html?model=02_Bolsos&marker=2'
  Aponta a câmara para o Marcador de Código de Barras nº 2 (3x3 PARITY65).