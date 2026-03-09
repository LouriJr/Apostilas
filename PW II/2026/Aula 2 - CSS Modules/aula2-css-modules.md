## 🎨 Passo 15: Estilizando com CSS Modules

No React, se criarmos um arquivo `style.css` comum, ele afetará o site inteiro. Para evitar que um componente "estrague" o visual do outro, usamos os **CSS Modules**.

### 1. Criando o Arquivo de Estilo

Dentro da pasta do seu componente (`src/components/ProfileCard/`), crie um novo arquivo chamado:
👉 `ProfileCard.module.css`

> **Atenção:** O nome deve terminar obrigatoriamente com `.module.css`.

### 2. Escrevendo o CSS

Abra o seu novo arquivo de CSS e adicione alguns estilos básicos para o nosso card:

```css
.card {
  background-color: #fffef2;
  filter: drop-shadow(4px 9px 10px #000000);

  height: 500px;
  width: 500px;

  border-radius: 16px;

  color: #000;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.foto {
  width: 200px;
}

.name {
  font-weight: bold;
  font-size: 1.2rem;
  margin: 5px 0;
}
```

## 🔗 Passo 16: Conectando o CSS ao Componente

Agora vem a diferença! Não importamos o CSS "solto". Nós o importamos como um **objeto**.

1. Volte ao arquivo `src/components/ProfileCard/ProfileCard.jsx`.
2. Altere o import e a forma de usar as classes:

JavaScript

```
// Importamos o estilo como um objeto chamado 'styles'
import styles from "./ProfileCard.module.css";

function ProfileCard(props) {
  return (
    /* Usamos styles.nomeDaClasse entre chaves */
    <div className={styles.card}>
      <img src={props.foto} alt={props.nome} className={styles.foto} />
      <p className={styles.name}>{props.nome}</p>
      <p>Idade: {props.idade}</p>
      <p>Profissão: {props.profissao}</p>
    </div>
  );
}

export default ProfileCard;
```

* * *

## 🔍 O que mudou?

- **className vs class:** No React, usamos `className` porque `class` é uma palavra reservada do JavaScript.
- **Escopo Local:** Se você abrir o navegador e inspecionar o elemento (F12), verá que o React gerou uma classe única como `_card_1abc2_1`. Isso garante que esse estilo **só se aplique a este componente**.
