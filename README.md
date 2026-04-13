# Pipeline de Acessibilidade — Jenkins

## Sobre
Pipeline Jenkins com stage de acessibilidade para a aplicação `http://teste-devops`.

## Ferramenta escolhida
**Pa11y** — ferramenta CLI open source de testes de acessibilidade,
compatível com Jenkins e de fácil integração via linha de comando.

## Como funciona
1. Verifica se o Pa11y já está instalado antes de instalar
2. Gera um relatório HTML salvo em `reports/acessibilidade/`
3. Exibe o resultado no log do Jenkins via terminal
4. Publica o relatório HTML como aba acessível na interface do Jenkins

## Padrão utilizado
**WCAG2AA** — padrão internacional de acessibilidade web,
cobre critérios como contraste de cores, textos alternativos e navegação por teclado.

## Pré-requisitos
- Jenkins com plugin **HTML Publisher** instalado
- Node.js disponível no agente
- Credencial SSH configurada no Jenkins com o ID `jenkins`
