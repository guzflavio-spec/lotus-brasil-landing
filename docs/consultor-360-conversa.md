# Projeto: Agente Consultor 360° (padrão McKinsey)

*Registro completo da conversa. Sessão de 21/11/2026, arquivo gerado em 25/11/2026.*
*Repositório: `guzflavio-spec/lotus-brasil-landing` · Branch: `ccr-9af39e3e-nuy0qs`*

---

## 1. Resumo

| Item | Estado |
|---|---|
| Pedido original | Criar um agente consultor de empresas padrão McKinsey, que analise a empresa em 360° |
| Entregue | Subagent `consultor-360` em `.claude/agents/consultor-360.md` + linha no `README.md` |
| Commit e push | Feitos na branch `ccr-9af39e3e-nuy0qs` (**antes** do teste pedido pelo usuário). Não foi aberto pull request |
| Teste com a Canto de Pano | Rodado **depois** do commit. O agente não identificou a empresa e entregou um relatório de "perfil provável", sem validade como diagnóstico real |
| Ajustes no agente | **Propostos, ainda não aplicados** (seção 5) |
| Pendente do usuário | Dados da Canto de Pano (Instagram, site, CNPJ, cidade) e liberação de rede para sites externos |

---

## 2. Linha do tempo da conversa

1. **Pedido:** "Criar um agente de consultor de empresa padrão McKinsey qual analisar a empresa em 360°".
2. **Exploração do repositório:** o repositório já tinha `.claude/skills`, `.claude/settings.json`, `.mcp.json`, `README.md` e `skills-lock.json` (configuração do Claude Code com skills, plugins e MCPs). Não havia pasta `.claude/agents/`.
3. **Criação do agente:** arquivo `.claude/agents/consultor-360.md` (conteúdo na seção 3) e acréscimo ao `README.md`.
4. **Stop hook:** pediu para commitar e enviar as mudanças. Foi feito o commit e o push para `ccr-9af39e3e-nuy0qs`.
5. **Usuário:** "Antes do commit, testar com a Canto de Pano". O commit já tinha saído, então o teste rodou depois. O `consultor-360` foi disparado em segundo plano em modo completo.
6. **Resultado do teste:** o agente não achou a empresa (relatório na seção 4).
7. **Proposta de melhoria:** três ajustes no agente (seção 5). Foi perguntado se devem ser aplicados antes ou depois de o usuário passar os dados da empresa. **Sem resposta até aqui.**
8. **Este pedido:** consolidar tudo em um `.md` para reunir num projeto só no Claude.

---

## 3. O agente `consultor-360`

**Arquivo:** `.claude/agents/consultor-360.md`
**Frontmatter:** `name: consultor-360` · `model: opus` · `tools: Read, Glob, Grep, Bash, Write, WebSearch, WebFetch`

### Como ele trabalha
- **Papel:** Engagement Manager sênior de consultoria estratégica de elite. Responde em português do Brasil, em tom executivo.
- **Princípios:**
  1. Resposta primeiro (Pirâmide de Minto).
  2. Estruturas MECE.
  3. Orientado por hipótese.
  4. "So what?" em cada dado.
  5. Rótulos `[FATO]` (com fonte), `[INFERÊNCIA]` e `[SUPOSIÇÃO]`; nunca inventar números, clientes ou fontes.
  6. Regra 80/20.
  7. Toda análise termina em ação, com responsável, prazo e métrica.
- **Fase 0, enquadramento:** no máximo 5 perguntas enxutas; escreve o SCQA (Situação, Complicação, Questão-chave, Hipótese). Se só receber o nome da empresa, segue com suposições explícitas.
- **Fase 1, coleta de evidências**, em ordem de confiabilidade:
  1. Arquivos do repositório.
  2. Site oficial e redes.
  3. Pesquisa externa.
  4. Dados do usuário.
- **Fase 2, diagnóstico em 12 dimensões**, cada uma com situação, evidências, nota de 1 a 5 e principal risco ou oportunidade:

| # | Dimensão | Frameworks úteis |
|---|---|---|
| 1 | Estratégia e proposta de valor | Playing to Win, 3 Horizontes, Canvas |
| 2 | Mercado | TAM/SAM/SOM, PESTEL, Cinco Forças |
| 3 | Clientes | Segmentação, JTBD, jornada |
| 4 | Concorrência | Mapa de posicionamento, benchmark |
| 5 | Produto e portfólio | BCG/GE, curva de valor |
| 6 | Marketing e marca | AARRR, brand equity |
| 7 | Vendas e receita | Árvore de receita, funil |
| 8 | Operações e cadeia de valor | Cadeia de valor, Lean |
| 9 | Finanças | ROIC, DRE, break-even, LTV/CAC |
| 10 | Organização e pessoas | 7S, RACI |
| 11 | Tecnologia, dados e digital | Maturidade digital |
| 12 | Risco, jurídico e ESG | Matriz de risco |

- **Fase 3, síntese:** SWOT enxuto cruzado com TOWS; causa-raiz (5 porquês); 2 a 4 opções estratégicas com uma recomendada.
- **Fase 4, plano:** matriz Impacto × Esforço; roadmap 30-60-90 dias e visão de 12 meses; 5 a 8 KPIs com baseline e meta; riscos e próximos passos.
- **Entregável:**
  1. Resumo executivo
  2. Contexto e SCQA
  3. Scorecard 360°
  4. Diagnóstico por dimensão
  5. Síntese
  6. Plano de ação
  7. Riscos e lacunas
  8. Anexo com fontes e cálculos
- **Modos:** rápido, completo (padrão), focado em uma dimensão e due diligence.
- **Limites:** não emite parecer contábil, jurídico ou fiscal; não envia dados internos a serviços externos; marca lacunas em vez de preencher com invenção; só grava arquivos (em `relatorios/<empresa>-diagnostico-360-<AAAA-MM-DD>.md`) se o usuário pedir.

### Como usar
```
Use o agente consultor-360 para fazer uma análise 360° da empresa X
```
Também funciona com `@consultor-360`. Se não aparecer na lista, reiniciar a sessão.

---

## 4. Teste com a Canto de Pano

**Pedido ao agente:** análise 360° completa, sem dados internos, pesquisando na web e usando premissas explícitas onde faltasse informação; em caso de homônimos, identificar a empresa mais provável.

**Resultado em uma frase:** o agente **não conseguiu identificar a empresa**. Em 15 buscas, nenhuma encontrou uma empresa chamada "Canto de Pano". Os acessos diretos a Instagram, possíveis domínios próprios e alguns portais de notícia foram bloqueados pela rede da sessão. Ele entregou então o diagnóstico de um **perfil provável** (microempresa de artesanato têxtil), com confiança **Baixa**.

> **Atenção:** o relatório abaixo **não vale como diagnóstico da empresa real**. Os achados específicos sobre a empresa são suposições. Os fatos de mercado citados vêm de fontes de busca e não foram conferidos por mim. O texto é saída do modelo (subagent), não uma verificação independente.

### Relatório do agente (texto integral)

# Diagnóstico 360°: "Canto de Pano"
*Modo completo. Data-base: 21/11/2026. Não usei dados internos; tudo vem de pesquisa web pública.*

> **Aviso antes de ler:** não consegui identificar a empresa. Fiz 15 buscas com variações de nome, categoria, cidade, CNPJ, marketplaces e redes sociais, e nenhuma achou uma empresa chamada "Canto de Pano". O acesso direto a sites (Instagram, possíveis domínios próprios, portais de notícia) foi bloqueado pela rede desta sessão. Por isso, o que vem abaixo é um **diagnóstico de um perfil provável** (arquétipo), com rótulos explícitos. **Não é** um diagnóstico verificado da empresa real. A confiança geral é **Baixa**.

---

## 1. Resumo executivo

**Conclusão:** a hipótese mais provável é uma microempresa brasileira de produtos têxteis artesanais (panos de prato, decoração em tecido, bonecas, enxoval) que vende sobretudo por Instagram, WhatsApp e marketplaces. Para um negócio assim, crescer com mais lucro depende de três movimentos: **(1) parar de ser invisível, (2) tirar volume do marketplace de ticket baixo e (3) montar receita recorrente B2B e de presentes.** [INFERÊNCIA, confiança Baixa]

**Achados principais**
1. **A marca não aparece na web pública.** Em 15 buscas, zero resultados com o nome exato: nenhum site, CNPJ com esse nome, perfil indexado ou review. Se a empresa existe, sua descoberta orgânica (SEO, marketplaces, reviews) é praticamente nula. [FATO sobre as buscas feitas; INFERÊNCIA sobre o porte]
2. **O principal canal do nicho fechou.** A Enjoei encerrou o Elo7 em 11/05/2026, após uma queda de receita de quase 40%. A plataforma chegou a ter cerca de 130 mil vendedores ativos, número que varia conforme a fonte. Isso deixou milhares de artesãos e compradores sem canal. [FATO: Canaltech, IstoÉ Dinheiro, Mercado & Consumo]
3. **A taxa da Shopee consome de 25% a 40% do preço em produtos baratos.** Pela tabela para CNPJ em vigor desde 03/2026 (20% + R$ 4 até R$ 79,99), um pano de R$ 19,90 perde 40% em taxa. Um kit de R$ 79,90 perde 25%. A **R$ 80,00** a taxa salta para 34%. [FATO: tabela segundo Ecommerce na Prática e ViniEnsina, com divergências entre fontes; cálculo no Anexo]
4. **O mercado é grande e fragmentado.** O artesanato movimenta de R$ 50 bi a R$ 102 bi por ano, cerca de 3% do PIB, com cerca de 8,5 milhões de artesãos. O e-commerce brasileiro cresceu 15,3% em 2025 e chegou a R$ 235,5 bi. [FATO: Sebrae, ABIACOM; os números do Sebrae divergem]
5. **Simulação de margem por canal** (preço de R$ 59,90, custo do produto de 35%, embalagem de R$ 2): margem de contribuição de 35% na Shopee, ~42% em loja própria com mídia paga e ~61% em venda direta por WhatsApp/Pix. [SUPOSIÇÃO de custos; cálculo no Anexo]

**Recomendação principal:** primeiro, **confirmar a identidade da empresa esta semana** (veja o item 7). Se o perfil for confirmado, seguir a estratégia **"canal próprio + B2B"**:
- montar kits presenteáveis entre R$ 69,90 e R$ 79,90;
- usar Instagram e WhatsApp como canal principal e o marketplace só para ganhar visibilidade;
- prospectar presentes corporativos e revenda em empórios e lojas de decoração.

**Impacto esperado** [SUPOSIÇÃO]: de +8 a +15 pontos percentuais na margem de contribuição média, se 30% do volume migrar do marketplace para venda direta, e ticket médio de +40% a +60% com os kits.

**Decisões que peço:** (a) confirmar quem é a empresa e (b) autorizar acesso ao Instagram ou ao site, ou enviar 5 dados básicos (item 7).

---

## 2. Contexto, pergunta-chave e premissas

**Como tratei os homônimos**
- Nenhum resultado com o nome exato.
- Nomes parecidos que descartei: "Canto do Pão", panificadora com CNPJ 32.965.488/0001-88 em Bossoroca/RS, **baixada em 11/10/2021**; "Coração de Pano", ateliê de bonecas de Dayanna Carlson; "Artes e Encantos de Pano", Jundiaí/SP; "Tiquinho de Pano"; "Pokin de Pano"; "Campista Minha Casa de Pano".
- **Por que escolhi o perfil "microempresa têxtil artesanal":** (i) o nome junta "canto" (cantinho, aconchego) e "pano" (tecido); (ii) todos os nomes parecidos que apareceram são ateliês têxteis artesanais; (iii) não ter nada indexado combina com um MEI ou ME que vive em Instagram e WhatsApp. [INFERÊNCIA, confiança Baixa]
- **Hipóteses alternativas ainda abertas:** loja física de tecidos ou armarinho de bairro; projeto cultural ou musical ("canto" no sentido de cantar); marca de outro país lusófono.

**SCQA**
- **Situação:** microempresa de artesanato têxtil, provavelmente liderada pela fundadora e vendendo por redes sociais e marketplaces. [SUPOSIÇÃO]
- **Complicação:** o Elo7 fechou em 05/2026, as taxas dos marketplaces generalistas subiram em 2026 e a marca não aparece em buscas. [FATO + INFERÊNCIA]
- **Questão-chave:** como crescer com mais margem sem depender de marketplace e de mídia paga cara?
- **Hipótese inicial:** o lucro está no ticket (kits e presentes), no canal direto e no B2B, não em volume no marketplace.

**Premissas assumidas (todas [SUPOSIÇÃO], a validar)**

| Item | Premissa |
|---|---|
| Porte | MEI ou ME, de 1 a 3 pessoas, faturamento abaixo de R$ 360 mil/ano |
| Produto | Têxteis artesanais para casa e presente, preço unitário de R$ 20 a R$ 80 |
| Canais | Instagram + WhatsApp + 1 marketplace (Shopee ou ML); ex-Elo7 possível |
| Custo do produto | ~35% do preço (insumo + mão de obra terceirizada) |
| Horizonte | 12 meses, caixa curto, sem capital externo |

---

## 3. Scorecard 360°
*As notas são hipotéticas (exceto a da dimensão 6) e valem para o arquétipo. Confiança Baixa em todas, salvo indicação.*

| # | Dimensão | Nota (1-5) | Tendência | Destaque |
|---|---|---|---|---|
| 1 | Estratégia e proposta de valor | 2 | → | Provável falta de nicho claro ("faz de tudo em tecido") |
| 2 | Mercado | 3 | ↗ | Mercado grande e fragmentado; e-commerce +15,3% em 2025 [FATO] |
| 3 | Clientes | 3 | → | Compra emocional e de presente; recompra baixa sem CRM |
| 4 | Concorrência | 2 | ↘ | Milhares de ateliês parecidos + produto industrial barato em marketplace |
| 5 | Produto e portfólio | 3 | → | Artesanal tem valor percebido; falta de kits limita o ticket |
| 6 | Marketing e marca | **1** | → | **Zero presença indexada** [FATO sobre as buscas; confiança Média] |
| 7 | Vendas e receita | 2 | ↘ | Ticket baixo; taxa da Shopee de 25% a 40% [FATO sobre a tabela] |
| 8 | Operações | 2 | → | Capacidade presa à mão de obra da fundadora |
| 9 | Finanças | 2 | ? | Margem provavelmente diluída por taxas e frete; não verificado |
| 10 | Organização e pessoas | 2 | → | Alta dependência da fundadora |
| 11 | Tecnologia e dados | 1 | → | Sem site ou CRM indexado |
| 12 | Risco e ESG | 3 | ↘ | Risco de plataforma provado pelo fim do Elo7; ESG artesanal favorável |

---

## 4. Diagnóstico por dimensão

**1. Estratégia: o jogo vencedor é ser presente afetivo de nicho, não pano barato.**
Contra o têxtil industrial de marketplace, o artesanal só ganha em história, personalização e embalagem. [INFERÊNCIA] O risco é ficar "no meio": nem barato, nem marca.

**2. Mercado: é grande, mas o canal de nicho encolheu.**
- [FATO] O artesanato equivale a cerca de 3% do PIB. O Sebrae estima o faturamento ora em R$ 102 bi, ora em R$ 50 bi. **Adoto R$ 50 bi como piso conservador.**
- [FATO] São cerca de 8,5 milhões de artesãos; 77% são mulheres e, para cerca de 2 em cada 3, é a principal fonte de renda (Sebrae).
- [FATO] O e-commerce somou R$ 204,3 bi em 2024 (ticket de R$ 492,40) e R$ 235,5 bi em 2025, alta de 15,3% (ABComm/ABIACOM).
- **E daí?** Há demanda, mas a oferta é enorme. A diferenciação vale mais que a demanda.

**3. Clientes: o comprador é quem dá presente, não quem consome.**
[SUPOSIÇÃO] Os segmentos prováveis são: mulheres de 30 a 60 anos que presenteiam (datas comemorativas, chá de casa nova); compradores corporativos (brindes de fim de ano); e revendas (empórios, lojas de decoração). Não há NPS nem dados de retenção.

**4. Concorrência: a briga é com ateliês parecidos e com o "bom o suficiente" industrial.**
- [FATO] Há concorrentes de nicho com modelo mais completo. O Ateliê Coração de Pano junta loja física e virtual, **cursos** e produtos para doll makers. O Artes e Encantos de Pano vende tecidos e aviamentos.
- [FATO] Depois do Elo7, os canais alternativos citados pela imprensa são a Tanlup (criativo nacional) e a Etsy (exportação).
- **E daí?** Cursos e moldes digitais são uma linha de alta margem que concorrentes já exploram.

**5. Produto: o kit presenteável é a alavanca de ticket.**
[INFERÊNCIA a partir do cálculo] Pela tabela da Shopee, o ponto ótimo de preço é **R$ 79,90** (taxa de 25%). Já **R$ 80 a R$ 99,99 é zona proibida**: a taxa vai para 31-34%.

**6. Marketing: a marca não existe para o Google.**
[FATO] Nenhuma ocorrência indexada do nome exato em 15 buscas. Ou a marca opera só dentro do Instagram, que não é indexado, ou o nome público é outro. A pesquisa no Instagram foi bloqueada nesta sessão. Os riscos são CAC alto e dependência de algoritmo.

**7. Vendas: em ticket baixo, o canal decide a margem.**
- [FATO] Taxa da Shopee para CNPJ desde 01/03/2026: 20% + R$ 4 até R$ 79,99; 14% + R$ 16 de R$ 80 a R$ 99,99. As fontes divergem (há quem cite +R$ 4,50, e a Omie cita outra faixa).
- [SUPOSIÇÃO] Em margem de contribuição: Shopee 35%, loja própria com mídia ~42%, WhatsApp/Pix ~61% (Anexo).

**8. Operações: o gargalo é a hora da artesã.**
[SUPOSIÇÃO] A produção é manual. Escalar exige padronizar SKUs, terceirizar a costura básica e manter a personalização como etapa final.

**9. Finanças: não encontrado.**
Não há DRE, faturamento ou CNPJ localizado. Para obter: extrato do marketplace (últimos 6 meses), DAS do MEI e planilha de custos por SKU.

**10. Organização: há risco de pessoa-chave.**
[SUPOSIÇÃO] Fundadora acumulando produção, atendimento e conteúdo. Sem processo documentado.

**11. Tecnologia: o mínimo viável está ausente.**
[INFERÊNCIA a partir do item 6] Não há site, catálogo indexável ou CRM. Opções baratas: catálogo do WhatsApp Business e uma loja em plataforma SaaS.

**12. Risco: o fim do Elo7 provou o risco de plataforma.**
- [FATO] Vendedores do Elo7 relataram que não conseguiram recuperar fotos, descrições e histórico para migrar.
- **E daí?** É preciso ter backup do catálogo e da base de clientes fora de qualquer plataforma.
- Também: LGPD na base de WhatsApp e registro da marca no INPI (sem busca feita; requer especialista).

---

## 5. Síntese

**SWOT (arquétipo)**

| Forças | Fraquezas |
|---|---|
| Produto artesanal com valor afetivo [SUP.] | Invisibilidade digital [FATO-busca] |
| Estrutura enxuta, custo fixo baixo [SUP.] | Ticket baixo e taxa alta de marketplace [FATO-tabela] |
| | Dependência da fundadora [SUP.] |

| Oportunidades | Ameaças |
|---|---|
| Compradores órfãos do Elo7 [FATO] | Taxas de marketplace subindo em 2026 [FATO] |
| E-commerce +15,3% em 2025 [FATO] | Têxtil industrial barato em marketplace [INF.] |
| Brindes corporativos de fim de ano (dez/2026) [INF.] | Mídia paga cada vez mais cara (motivo citado pela Enjoei para fechar o Elo7) [FATO] |
| Cursos e moldes digitais [FATO-concorrente] | |

**TOWS: opções geradas**
- **FO:** usar o valor afetivo para captar quem comprava no Elo7 → kits de presente + perfis em Tanlup/Etsy.
- **FA:** fugir da guerra de preço → B2B corporativo e revenda com preço de atacado.
- **WO:** atacar a invisibilidade → Google Perfil da Empresa, catálogo indexável, SEO de cauda longa ("pano de prato bordado personalizado").
- **WA:** reduzir o risco de plataforma → base própria de clientes no WhatsApp/e-mail com consentimento (LGPD).

**Causas-raiz (5 porquês)**
1. *Margem baixa* → muito volume no marketplace → é o único canal com tráfego → a marca não é encontrada fora dele → falta catálogo indexável e conteúdo de busca → **a fundadora não tem tempo nem método de marketing.**
2. *Ticket baixo* → venda por unidade → não há kits nem embalagem de presente → o portfólio foi pensado como produto, não como ocasião → **falta pensar o produto pela "missão de presente" do cliente.**

**Opções estratégicas**

| Opção | Prós | Contras | Investimento | Risco |
|---|---|---|---|---|
| A. Escalar no marketplace | Tráfego pronto | Taxa de 25-40%, guerra de preço | Baixo | Alto (plataforma) |
| **B. Canal próprio + kits de presente** | Margem até ~61%, base própria | Exige conteúdo constante | Baixo-médio (R$ 2-5 mil) [SUP.] | Médio |
| **C. B2B: corporativo e revenda** | Ticket alto, previsível | Ciclo de venda, capital de giro | Baixo | Médio |
| D. Cursos e moldes digitais | Margem bruta muito alta, escalável | Exige audiência antes | Médio | Médio-alto |

**Recomendação: B + C, com o marketplace (A) só como vitrine.** D fica para o horizonte 2, depois de ter audiência. [Confiança Baixa, porque depende da identificação]

---

## 6. Plano de ação

**Impacto × Esforço**
- **Quick wins:** confirmar a identidade e os dados; reprecificar kits para R$ 69,90-79,90; catálogo do WhatsApp Business; Google Perfil da Empresa; backup do catálogo.
- **Apostas grandes:** campanha de brindes corporativos para o fim de ano; loja própria.
- **Preenchimentos:** perfil na Tanlup/Etsy; registro da marca no INPI.
- **Descartar por ora:** mídia paga em escala; ampliar SKUs unitários baratos.

**Roadmap**

| Prazo | Iniciativa | Responsável sugerido | Entregável |
|---|---|---|---|
| Semana 1 | Validar identidade e baseline (item 7) | Fundadora + consultor | Ficha com 5 dados |
| 30 dias | 3 kits presenteáveis abaixo de R$ 80; backup do catálogo; catálogo no WhatsApp; Google Perfil | Fundadora | Kits no ar; catálogo exportado |
| 30 dias | Lista de 50 empresas locais para brinde de fim de ano + proposta em PDF | Fundadora / freelancer comercial | 50 contatos, 10 propostas |
| 60 dias | Loja própria simples + 8 posts/mês com foco em presente | Freelancer de marketing | Loja no ar; conversão medida |
| 90 dias | 5 revendas (empórios e decoração) em consignação ou atacado | Fundadora | 5 pontos de venda |
| 12 meses | Avaliar linha de cursos e moldes; terceirizar a costura básica | Fundadora | Decisão go/no-go |

**KPIs** (baseline: **não encontrado**, medir na semana 1)

| KPI | Meta 90 dias [SUP.] | Frequência |
|---|---|---|
| **Norte:** margem de contribuição total (R$/mês) | +25% sobre o baseline | Mensal |
| Ticket médio | +40% | Semanal |
| % da receita fora do marketplace | ≥ 50% | Mensal |
| Receita B2B (corporativo + revenda) | ≥ 20% da receita | Mensal |
| Base própria de clientes com consentimento | +300 contatos | Mensal |
| Taxa de recompra em 90 dias | ≥ 15% | Trimestral |
| Horas da fundadora em produção | -20% | Mensal |

---

## 7. Riscos, lacunas e próximos passos

**Maior risco deste relatório:** a empresa real pode não ser uma microempresa têxtil. Nesse caso, o diagnóstico perde a validade.

**Lacunas e como fechar (prioridade)**
1. **Identidade:** @ do Instagram, CNPJ ou site oficial e cidade. **Isso eleva a confiança de Baixa para Média.**
2. **Liberar na rede da sessão:** instagram.com, o domínio da empresa, mercadoeconsumo.com.br e jornaldebrasilia.com.br (todos bloqueados aqui).
3. **Dados mínimos:** faturamento mensal (6 meses), receita por canal, top 10 SKUs com preço e custo, número de clientes e recompra, horas de produção por peça.
4. Tabela oficial atual da Shopee e do Mercado Livre (as fontes secundárias divergem).

**Decidir esta semana:** confirmar a empresa e escolher entre aprofundar (com os dados) ou validar só as hipóteses de canal e ticket.

---

## 8. Anexo

**Cálculos** (Python, tabela da Shopee para CNPJ: <R$ 80 = 20% + R$ 4; R$ 80-99,99 = 14% + R$ 16)

| Preço | Taxa R$ | Taxa % |
|---|---|---|
| 19,90 | 7,98 | 40,1% |
| 39,90 | 11,98 | 30,0% |
| 59,90 | 15,98 | 26,7% |
| 79,90 | 19,98 | 25,0% |
| 80,00 | 27,20 | 34,0% |
| 89,90 | 28,59 | 31,8% |

- Margem de contribuição = preço − custo do produto (35%) − embalagem (R$ 2) − custo do canal. Com preço de R$ 59,90:
  - Shopee: R$ 20,96 (35,0%);
  - loja própria com 5% de gateway + 15% de mídia [SUP.]: R$ 24,96 (41,7%);
  - WhatsApp/Pix a 1% [SUP.]: R$ 36,34 (60,7%).
- Crescimento do e-commerce: 235,5 / 204,3 − 1 = 15,3%.

**Fontes** (todas acessadas em 21/11/2026, via buscador; o acesso direto às páginas foi bloqueado)
- Elo7: [Canaltech](https://canaltech.com.br/mercado/o-que-aconteceu-com-a-elo7-enjoei-encerra-operacoes-do-marketplace/), [IstoÉ Dinheiro](https://istoedinheiro.com.br/enjoei-anuncia-encerramento-das-operacoes-da-plataforma-elo7-2), [Mercado & Consumo](https://mercadoeconsumo.com.br/11/05/2026/ecommerce/enjoei-encerra-operacoes-da-elo7-apos-queda-de-quase-40-na-receita/), [Times Brasil](https://timesbrasil.com.br/empresas-e-negocios/enjoei-fecha-elo7-o-que-acontece-com-pedidos-clientes-e-vendedores/), [Jornal de Brasília](https://jornaldebrasilia.com.br/noticias/economia/marketplaces-de-artesanato-ganham-espaco-apos-o-fim-da-elo7/), [Nuvemshop](https://www.nuvemshop.com.br/blog/como-vender-no-elo7/)
- Shopee: [Ecommerce na Prática](https://ecommercenapratica.com/blog/taxa-shopee/), [ViniEnsina](https://viniensina.com.br/?p=4619), [Omie](https://www.omie.com.br/blog/como-vender-na-shopee-com-cnpj/)
- Mercado: [Agência Sebrae](https://agenciasebrae.com.br/cultura-empreendedora/artesanato-uma-economia-tecida-a-maos), [Data Sebrae](https://datasebrae.com.br/wp-content/uploads/2024/07/Impulsionar-Negocios-2025-Artesanato.pdf), [Gazeta SP](https://www.gazetasp.com.br/economia/artesanato-e-responsavel-por-fatia-gigante-do-pib-nacional/), [Mercado & Consumo, e-commerce 2024](https://mercadoeconsumo.com.br/14/01/2025/ecommerce/e-commerce-brasileiro-cresce-105-e-fatura-r-2043-bilhoes-em-2024), [GiroNews](https://gironews.com/varejo-digital/e-commerce-projeta-faturamento-superior-a-r-234-bilhoes-em-2025/)
- Nomes parecidos: [CNPJ Canto do Pão](https://cnpj-api.com/en/cnpj/32965488000188), [Coração de Pano](https://coracaodepano.com.br/quem-somos/), [Artes e Encantos de Pano](https://www.ateliearteseencantosdepano.com.br/)

### Auto-avaliação do processo (escrita pelo próprio agente)

**O que faltou nas instruções**
1. **Não há critério para "empresa não encontrada".** A instrução de seguir com suposições entra em conflito com a de nunca inventar. Faltou uma regra do tipo: "se a confiança na identificação for Baixa, entregue um relatório curto de arquétipo mais as perguntas, não o formato integral". O formato de 12 dimensões com notas dá uma aparência de rigor que o dado não sustenta.
2. **Não há critério de parada da busca** nem um checklist de identificação (CNPJ, INPI, Google Maps, Instagram, Reclame Aqui). Parei em 15 buscas por julgamento próprio.
3. **Faltou um modo "arquétipo setorial"**, com um padrão de como rotular notas hipotéticas no scorecard.

**O que faltou nas ferramentas**
1. **Rede restrita:** o WebFetch e o curl foram bloqueados para Instagram, os possíveis domínios da empresa e portais de notícia. Não deu para ler nenhuma fonte primária, só os resumos do buscador.
2. **Sem acesso a bases estruturadas:** Receita Federal (CNPJ por razão social), INPI, Google Maps e Reclame Aqui.
3. **O buscador devolve resumos já interpretados** (às vezes em inglês e com divergências), o que fragiliza a rotulagem de [FATO]. O ideal seria ler a página original.

---

## 5. Melhorias propostas para o agente (ainda não aplicadas)

1. **Regra de empresa não identificada:** se a confiança na identificação for Baixa, entregar apenas um relatório curto de arquétipo, **sem notas no scorecard**, mais as perguntas necessárias para destravar a análise.
2. **Checklist de identificação e limite de buscas:** CNPJ, INPI, Google Maps, Instagram, Reclame Aqui, com um teto de buscas antes de parar e perguntar.
3. **Rótulo padrão para notas hipotéticas:** quando houver scorecard sem dados, marcar cada nota como "hipotética" de forma visível.

---

## 6. Próximos passos

- [ ] **Usuário:** informar o @ do Instagram, o site ou o CNPJ da Canto de Pano, mais a cidade.
- [ ] **Usuário:** liberar na rede do ambiente o Instagram e o domínio da empresa, se os dados acima não forem suficientes.
- [ ] **Usuário:** decidir se os três ajustes da seção 5 entram agora ou depois de passar os dados da empresa.
- [ ] Aplicar os ajustes em `.claude/agents/consultor-360.md` e fazer novo commit na branch `ccr-9af39e3e-nuy0qs`.
- [ ] Rodar o `consultor-360` de novo na Canto de Pano com os dados reais e validar o resultado.
- [ ] Se for aprovado, decidir se abre pull request (não foi aberto).

---

## 7. Arquivos e referências

| Caminho | O que é |
|---|---|
| `.claude/agents/consultor-360.md` | Definição do agente (commitada e enviada) |
| `README.md` | Ganhou uma linha sobre o agente (commitada e enviada) |
| `docs/consultor-360-conversa.md` | Este documento (ainda **não** commitado) |
| Branch `ccr-9af39e3e-nuy0qs` | Branch de desenvolvimento desta sessão |
