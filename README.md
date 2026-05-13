# qa-web-melissa
# 🧪 Test Report — Melissa.com.br

> **Projeto:** Testes Manuais de Interface e Usabilidade  
> **Site testado:** [melissa.com.br](https://www.melissa.com.br)  
> **Tipo de teste:** Manual + Performance  
> **Status geral:** Falhas Críticas Identificadas

---

## 📋 Sumário Executivo

Este relatório documenta os defeitos encontrados durante a execução de testes manuais no site **melissa.com.br**. Foram executados 94 testes, que cobriram as áreas de navegação, página de produtos busca, filtros, login e conta responsividade mobile e performance. Testes de checkout foram excluídos do escopo por envolverem simulação de compra real.
Todos os casos de teste estão disponiveis na [planilha de testes](https://docs.google.com/spreadsheets/d/1K0Ubd2suB5Pse3-bkYWqtvorbG63uWMmwzRCcUpS4M0/edit?usp=sharing).

| Métrica | Valor |
|---|---|
| Total de casos com falha documentados | 7 |
| Severidade Alta | 5 |
| Severidade Média | 1 |
| Severidade Baixa | 1 |

---

## 🐛 Defeitos Encontrados

### CT-013 — Botão "Coleções": comportamento inconsistente ao clicar

| Campo | Detalhe |
|---|---|
| **ID** | CT-013 |
| **Módulo** | Navegação / Menu Principal |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
O botão "Coleções" exibe corretamente um submenu de coleções ao passar o mouse (*hover*). Porém, ao clicar no botão, o usuário é redirecionado para uma página de sapatos genérica, e não para a listagem de coleções esperada.

**Resultado Esperado:** Ao clicar em "Coleções", o usuário deve ser direcionado à página de coleções.  
**Resultado Obtido:** O clique redireciona para uma página de listagem de sapatos.

---

### CT-016 — Botão "Histórias": redirecionamento incorreto

| Campo | Detalhe |
|---|---|
| **ID** | CT-016 |
| **Módulo** | Navegação / Menu Principal |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
O botão "Histórias" exibe o submenu correto ao passar o mouse. Contudo, ao clicar, o usuário é levado à página "Novidades", que é uma seção diferente do site.

**Resultado Esperado:** Navegação para a página "Histórias".  
**Resultado Obtido:** Redirecionamento para a página "Novidades".

---

### CT-024 — Busca com caracteres especiais: resultados inconsistentes

| Campo | Detalhe |
|---|---|
| **ID** | CT-024 |
| **Módulo** | Busca / Search |
| **Severidade** | 🟢 Baixa |
| **Ambiente** | Desktop |

**Descrição:**  
A funcionalidade de busca apresenta comportamento inconsistente ao receber caracteres especiais como entrada.

| Entrada | Resultado Obtido | Resultado Esperado |
|---|---|---|
| `#` | Retorna produtos (sandálias) | Mensagem de "Desculpe, não foram encontrados resultados para "#" " |
| `@`, `%`, `&` | Exibe mensagem de "Desculpe, não foram encontrados resultados para "@,$,&" " | "Desculpe, não foram encontrados resultados para "@,$,&" " |

A inconsistência indica falta de tratamento e sanitização adequados na camada de busca.

---

### CT-081 — Filtro de preço não exibe resultados e trava demais filtros

| Campo | Detalhe |
|---|---|
| **ID** | CT-081 |
| **Módulo** | Filtros / Listagem de produtos |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
Ao aplicar o filtro de preço na listagem de produtos, nenhum resultado é exibido, mesmo havendo produtos disponíveis no intervalo selecionado. Além disso, após a aplicação do filtro de preço, os demais filtros ficam inacessíveis, impossibilitando refinar a pesquisa.

**Resultado Esperado:** Filtro de preço exibe os produtos correspondentes e permite combinação com outros filtros.  
**Resultado Obtido:** Sem resultados exibidos e bloqueio dos demais filtros.

---

### CT-083 — Múltiplos filtros exigem adição um por vez

| Campo | Detalhe |
|---|---|
| **ID** | CT-083 |
| **Módulo** | Filtros / Usabilidade |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
Embora seja possível combinar múltiplos filtros simultaneamente, o sistema força o usuário a aplicar um filtro por vez, sem a possibilidade de selecionar vários antes de confirmar. Isso fragmenta a experiência e aumenta o número de interações necessárias.

**Resultado Esperado:** Interface que permita selecionar múltiplos filtros e aplicá-los de uma vez.  
**Resultado Obtido:** Cada filtro é aplicado individualmente, recarregando a página a cada seleção.

---

### CT-090 — Pesquisa no mobile sobreposta pela home

| Campo | Detalhe |
|---|---|
| **ID** | CT-090 |
| **Módulo** | Mobile / Responsividade |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Mobile |

**Descrição:**  
Ao realizar uma pesquisa no dispositivo mobile, a página home permanece visível e responsiva ao fundo, causando sobreposição visual e prejudicando a fluidez da navegação.

**Resultado Esperado:** A tela de busca deve ocupar toda a tela, ocultando a home.  
**Resultado Obtido:** Home visível e interativa simultaneamente à busca, gerando confusão visual.

---

### CT-092 — Performance crítica no Lighthouse (14/100)

| Campo | Detalhe |
|---|---|
| **ID** | CT-092 |
| **Módulo** | Performance / Web Vitals |
| **Severidade** | 🟠 Média |
| **Ambiente** | Desktop (Lighthouse) |

**Descrição:**  
O teste de performance realizado via Google Lighthouse retornou uma pontuação de **14 pontos**, muito abaixo da meta estabelecida de **≥70 pontos**. Esse resultado indica problemas graves de otimização que impactam diretamente a experiência do usuário e o posicionamento em mecanismos de busca (SEO).

| Indicador | Meta | Obtido |
|---|---|---|
| Performance Score | ≥ 70 | 14 |

**Impactos possíveis:** Carregamento lento de recursos, imagens não otimizadas, JavaScript bloqueante, ausência de cache eficiente, layout shifts (CLS elevado).

---

## ✅ O que pode ser feito:

1. **Revisão dos links do menu principal** — Verificar mapeamento de rotas dos botões "Coleções" e "Histórias".
2. **Sanitização da busca** — Implementar tratamento de caracteres especiais com retorno consistente ao usuário.
3. **Correção do filtro de preço** — Investigar a lógica de filtragem e garantir que não bloqueie outros filtros.
4. **UX de filtros múltiplos** — Adotar padrão de seleção múltipla com botão de confirmação.
5. **Sobreposição mobile** — Implementar foco exclusivo na tela de busca em dispositivos móveis.
6. **Otimização de performance** — Priorizar LCP, redução de JavaScript e otimização de imagens para atingir score ≥ 70 no Lighthouse.

---

*Relatório gerado para fins de portfólio — Testes executados manualmente, sem automação.*
Entrei em contato com a equipe da Melissa e eles responderam agradecendo :) 
<img width="1085" height="478" alt="image" src="https://github.com/user-attachments/assets/e21d6a79-ee72-45cb-afff-2e4bc8173f21" />
