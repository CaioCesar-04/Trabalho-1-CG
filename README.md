# Trabalho de Computação Gráfica: Reflexo e Transparência

Efeito de vidro escuro (com reflexo e transparência) em um plano, feito em WebGL 2 e GLSL.

## Enunciado

**Objetivo:** desenvolver um efeito de reflexo e transparência em um plano utilizando WebGL/GLSL. O shader deve simular um material translúcido com reflexo, como por exemplo um vidro escuro.

**Requisitos técnicos:**

1. **Shader customizado**
   - Implementação própria dos shaders vertex e fragment.
   - O shader deve calcular a reflexão e a transparência com base no ângulo de visão (não deve ser utilizado texturas prontas).
2. **Reflexo e transparência dinâmicos**
   - O reflexo e a transparência devem ser simulados utilizando um framebuffer renderizado a partir da cena (não usar cube map), usando renderização em vários passos (como foi feito usando shadow map). É permitido usar stencil buffer para transparência.
3. **Transparência controlada**
   - A transparência deve ser ajustável por meio de um uniform.
4. **Textura padrão**
   - Todos os objetos devem possuir uma textura padrão, inclusive o próprio vidro.
5. **Utilizar clipping plane** (não é permitida a seleção por "if" de objetos que serão renderizados).
6. **Câmera que permita movimento flyby** (permitida a cópia da internet).

**Entrega e demonstração:** demonstração em tempo real do shader aplicado em um plano dentro de uma cena contendo pelo menos dois objetos (com o plano dividindo eles).

## Como funciona

A cena tem um chão, uma pirâmide de um lado e um cubo do outro, separados por um vidro. Cada quadro é desenhado em 3 passes:

1. **Reflexo:** a cena espelhada pelo plano do vidro é renderizada num framebuffer. O clipping plane mantém só o lado da câmera.
2. **Transparência:** a cena é renderizada em outro framebuffer. O clipping plane mantém só o que está atrás do vidro.
3. **Tela:** a cena inteira e o vidro, que junta as duas texturas com a sua textura própria. O peso do reflexo vem do ângulo de visão (Fresnel/Schlick) e do uniform `transparencia`.

No código, as marcas `[R1]` a `[R6]` indicam onde cada requisito é cumprido.

## Controles

| Ação | Comando |
|---|---|
| Olhar ao redor | arrastar o mouse |
| Andar / subir e descer | W A S D / Q E (Shift = mais rápido) |
| Girar | setas |
| Transparente ↔ reflexo | slider do vidro |
| Distância dos objetos ao vidro | sliders do painel |
| Testar o clipping na tela | C |
| Ver só o reflexo / só a transparência no vidro | V |

## Como executar

As texturas precisam ser servidas por HTTP. Abra `projeto/index.html` com a extensão **Live Server** do VS Code, ou rode dentro da pasta `projeto/`:

```bash
python -m http.server 8000
```

e acesse `http://localhost:8000`.

## Estrutura

```
projeto/
├── index.html      shaders e código do trabalho
├── Common/         MV.js e initShaders.js (bibliotecas da disciplina)
└── texturas/       texturas dos objetos e do vidro
```
