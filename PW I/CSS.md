## CSS
Durante a aula passada estudamos o CSS, sua configuração e seu uso, agora vamos estudar as principais propriedades do CSS, são elas:

1. **Cor (color):** Define a cor do texto.
``` HTML
    //index.html
    <div class="container">
        <p>Texto de exemplo</p>
    </div>
```
``` CSS
    /* index.css */
    .container{
        color: red;
    }
```
2. **Fundo (background-color):** Controla a cor de fundo de um elemento.
``` HTML
    //index.html
    <div class="container">
        <p>Texto de exemplo</p>
    </div>
```
``` CSS
    /* index.css */
    .container{
        background-color: red;
    }
```
3. **Fonte (font):** Define a família de fonte, tamanho e outros atributos de texto.

3.1. ***font-family*** 
``` CSS
    /* index.css */
    .container{
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif
    }
```
3.2. ***font-size*** 
``` CSS
    /* index.css */
    .container{
        font-size: 50px;
    }
```
3.2. ***font-weight*** 
``` CSS
    /* index.css */
    .container{
        font-weight: 500;
    }
```

4. **Margens (margin):** Controla o espaço ao redor do elemento.
``` HTML
    //index.html
    <div class="container">
        <p class="text">Texto de exemplo 1</p>
        <p class="text">Texto de exemplo 2</p>
    </div>
```
``` CSS
    /* index.css */
    .text {
        margin-top: 15px;
        margin-right: 15px;
        margin-bottom: 15px;
        margin-left: 15px;
        margin: 10px 10px 10px 10px;
    }
```
5. **Preenchimento (padding):** Controla o espaço interno de um elemento em relação à sua borda.
``` CSS
    /* index.css */
    .container {
        padding: 10px 11px 12px 13px;
        padding-left: 10px;
        padding-right: 10px;
        padding-top: 10px;
        padding-bottom: 10px;
    }
```
6. **Borda (border):** Define as propriedades da borda do elemento, como largura, estilo e cor.
7. **Largura e altura (width e height):** Define as dimensões do elemento.
8. **Posição (position):** Controla como o elemento é posicionado em relação aos seus elementos pais.
9. **Exibição (display):** Define como o elemento deve ser exibido, como bloco, linha ou em linha.
10. **Flutuação (float):** Controla como um elemento deve se comportar em relação aos outros elementos ao seu redor.
11. **Opacidade (opacity):** Define a transparência do elemento.
12. **Z-index:** Controla a ordem de empilhamento dos elementos em camadas sobrepostas.
13. **Texto (text):** Define propriedades de texto, como espaçamento entre linhas (line-height) e alinhamento de texto.
14. **Sombra (box-shadow e text-shadow):** Adiciona sombras aos elementos, tanto caixas como texto.
15. **Transições (transition):** Permite criar animações suaves entre diferentes estados de um elemento.
16. **Transformações (transform):** Aplica transformações 2D e 3D a elementos, como rotação, escala e translação.
17. **Gradientes (linear-gradient e radial-gradient):** Define gradientes de cor para elementos.
18. **Seletores (selectors):** Permitem direcionar elementos específicos para aplicar estilos com base em suas classes, IDs ou hierarquia.
19. **Mídia (media):** Define estilos específicos para diferentes tamanhos de tela ou tipos de dispositivos.
20. **Variáveis CSS (CSS variables):** Permite criar variáveis personalizadas para reutilizar valores em várias partes do seu código CSS.
