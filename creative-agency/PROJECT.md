# Projeto: Agência Criativa com IA

Documento único com tudo o que foi decidido e construído nesta conversa (24 e 25/11/2026).
Pensado para ser anexado como conhecimento de um Projeto no Claude.

> Regra permanente do usuário: **não tem mais nenhum vínculo com a empresa anterior e não quer
> ouvir falar dela.** Nunca sugerir, retomar ou usar skills, marca ou materiais dela.
> Isso já foi gravado em Mem0, Vertiso Memory, Mem e Gryz.

---

## 1. Resumo executivo

- Objetivo: montar uma **agência criativa assistida por IA** (um agente do Claude Code com
  papéis de agência), com biblioteca de prompts de vídeo/imagem e um método que force
  **ideias não óbvias**.
- Ponto de partida: um vídeo de 15 s em 9:16 (anúncio de Black Friday da ElevenLabs, com
  personagem em selfie POV na Times Square). A legenda do arquivo ("Postcards from our After
  Hours event") **não correspondia** ao conteúdo do vídeo.
- Entregue: agente `creative-agency`, playbook de prompts, templates, 3 bibliotecas de prompts
  com licença CC BY 4.0 e o método de criatividade (premissa do time). Tudo na branch
  `ccr-2be0a9a0-fnjfcb` do repositório do usuário. Nenhum PR aberto.
- Em andamento: campanha para a **Canto de Pano**. Faltam dados da marca (ver seção 8).

---

## 2. Análise do vídeo de referência

Dados técnicos: 15,0 s, 720×1280 (9:16), 24 fps, H.264, com áudio AAC.

| Trecho | O que acontece | Como se faz |
|---|---|---|
| 0–3 s | Selfie POV: garota animada em Times Square, aponta para painéis "50% OFF" | Clipe de IA (imagem para vídeo) |
| 3–9 s | Whip pan até um painel gigante com o rosto dela e "BLACK FRIDAY 50% OFF" | Clipe de IA, mesma personagem |
| 9–12 s | Câmera baixa olhando o céu, ela se inclina sobre a lente | Clipe de IA |
| 12–15 s | Fundo preto, texto branco e botão "Claim offer" | Edição, **não é IA** |

---

## 3. Como produzir um vídeo assim (passo a passo)

1. **Roteiro** em 3 beats mais end card. Clipes de 5–8 s.
2. **Personagem de referência:** gerar uma selfie vertical 9:16 (imagem). Ela vira o primeiro
   quadro e mantém a mesma pessoa em todos os clipes.
3. **Clipes:** imagem para vídeo no ElevenLabs Creative, 9:16. Veo 3.1, Seedance 2.x ou Kling 3
   funcionam bem para selfie e whip pan. Fazer 2–3 takes por clipe.
4. **Áudio:** Veo e Seedance geram som ambiente e fala. Para controle total, usar TTS e
   SFX/música do ElevenLabs.
5. **Montagem:** Studio do ElevenLabs, CapCut ou Descript. Cortes secos na whip pan, legendas e
   end card.
6. **Exportação:** 9:16 1080p. Upscale só se a plataforma pedir.

Para **recap de evento ("postcards")**: usar fotos reais do evento como primeiro quadro
(imagem para vídeo), 3–4 s por clipe, música única e cartão final. Evita gerar pessoas falsas
e custa menos.

---

## 4. Planos e custos do ElevenLabs

Preços conferidos em 24/11/2026 na página oficial. Confirmar no app antes de assinar.

| Plano | Preço | Vídeo por mês (leitura da tabela da página) | Observação |
|---|---|---|---|
| Free | US$ 0 | quase nada | Só uso pessoal, sem vídeo de verdade |
| Starter | US$ 6 | ~211 s em Fast/Lite, ~49 s premium | 720p, licença comercial |
| **Creator** | **US$ 22** (US$ 11 no 1º mês) | ~705 s Fast/Lite, ~165 s premium | Todos os modelos, 1080p. **Recomendado** |
| Pro | US$ 99 | ~3.525 s Fast/Lite, ~825 s premium | 4K, só com volume |

- Black Friday (até 1º/12): Creator anual a US$ 8,25/mês no 1º ano.
- Um vídeo de 15 s precisa de ~8–10 s gerados; com 3–4 tentativas por clipe, ~45 s.
- **Estimativa** (derivada da tabela, não de preço por geração): modelos Fast/Lite ~US$ 1,40 de
  cota do Creator; modelos premium ~US$ 6. Realista: US$ 11–22 no primeiro mês e US$ 1,50–6
  por vídeo pronto.

---

## 5. Prompts abertos no GitHub

Copiados com atribuição (todos CC BY 4.0), em `creative-agency/prompts/sources/`:

| Repositório | Uso |
|---|---|
| lichamnesia/awesome-ad-video-prompts | Prompts de anúncio em vertical, UGC, POV, selfie com whip pan |
| uniqaiapp/awesome-ai-video-prompts | Kling 3, Veo 3, Wan 2.5, Runway, Seedance, com modelo e motivo |
| ericgood/seedance-prompt | Comparativo de modelos e prompts de Seedance |

Só links (licença diferente ou não verificada): ai-boost/awesome-image-video-prompts (GPL-3.0),
YouMind-OpenLab/awesome-seedance-2-prompts, renoise-ai/awesome-seedance-prompts,
jnMetaCode/ai-shortfilm-prompts, geekjourneyx/awesome-ai-video-prompts,
ai9app/AI-Cinematic-Prompt-Director, HitPaw-Official/awesome-ai-video-prompts.

---

## 6. O agente criativo

Arquivo: `.claude/agents/creative-agency.md`.

**Papéis:** Account Manager, Strategist, Creative Director, Copywriter, Art Director, Video
Producer, Producer.

**Pipeline:** brief → estratégia → conceitos (método da premissa) → execução (roteiro, direção
visual, shot list) → prompts de produção → entrega com plano e custo.

**Regras duras:** usar só material de marca que o usuário der no brief; não inventar fatos,
números ou depoimentos; não gerar depoimentos falsos nem imitar pessoas/organizações; gastar
créditos de ferramentas só com OK e estimativa; prompts de vídeo em inglês, com formato e
duração, uma ação e um movimento de câmera por plano, personagem idêntico entre planos; custos
só de fontes conferidas na sessão.

**Arquivos do projeto**

```
.claude/agents/creative-agency.md    o agente
creative-agency/README.md            visão geral
creative-agency/PROJECT.md           este documento
creative-agency/prompts/CREATIVE-PREMISE.md   premissa e método
creative-agency/prompts/PLAYBOOK.md           fórmulas e fluxo de prompts
creative-agency/prompts/templates/            templates prontos
creative-agency/prompts/sources/              bibliotecas CC BY 4.0
creative-agency/prompts/ATTRIBUTION.md        créditos e licenças
```

---

## 7. Premissa do time (inegociável)

**Ideias não óbvias. Criatividade com inteligência. Criatividade assistida por IA.**

Método, nesta ordem:

1. **Lista do óbvio:** 10 ideias que qualquer um teria, incluindo o que uma IA responderia por
   padrão. 
2. **Lista de banidas:** essas e as parecidas.
3. **Mineração de insight:** 5 tensões reais do público; ficar com as 2 menos discutidas.
4. **Rotas forçadas:** inversão, restrição absurda, formato emprestado de outro mundo, zoom,
   o meio como mensagem, participação do público.
5. **Ataque:** argumentar contra cada ideia como cliente hostil, espectador entediado e
   concorrente.
6. **Nota de obviedade (1–5):** só passam 4–5, ou 3 com plano de correção.
7. **Checagem de inteligência:** insight, por que funciona, como medir, risco. Sem os quatro,
   a ideia não está pronta.
8. **Protótipo com IA:** o teste mais barato (keyframe, clipe de 5 s, leitura do roteiro).

Papel da IA: divergir, atacar as próprias ideias, combinar rotas e produzir. A escolha final é
sempre justificada por uma pessoa. Nenhum primeiro rascunho de IA vai como conceito.

Cartão de conceito: nome, ideia em uma linha, insight, por que funciona, obviedade (1–5), rota
usada, gancho (2 s), protótipo com IA, risco e correção, alternativas descartadas.

---

## 8. Campanha Canto de Pano (estado atual)

**Pedido do usuário:** criar uma nova campanha. Respostas dadas: objetivo **vender mais**;
canais **multicanal**; para descobrir o que a marca vende, o usuário pediu para buscar na
memória do Claude e varrer as conversas dos últimos 45 dias.

**Resultado da varredura**
- Mem0, Vertiso, Mem e Gryz: nenhum registro sobre a Canto de Pano.
- Das 10 conversas dos últimos 45 dias, só a "Agente consultor McKinsey 360°" menciona a marca
  (diagnóstico 360°). Ela também não achou a empresa e ficou esperando os dados.
- A busca na web só trouxe páginas genéricas sobre panos e tecidos.
- Conclusão: **não há fatos confirmados sobre a marca.** Nada abaixo é fato.

**Conceitos provisórios** (baseados só no nome; assumem negócio têxtil/casa)

1. **"Pano de Prova"** (obviedade 4): o pano de prato vira canal de venda, com QR e frase impressos;
   o dono indica a marca ao próximo. Gancho: "Seu pano de prato nunca foi escolhido. O seu pode
   ser." Teste com IA: clipe de 5 s de uma cozinha com o pano como protagonista.
2. **"Canto" duplo** (obviedade 4): canto do pano e canto de cantar; cada peça traz uma cantiga
   de casa em áudio por QR. Gancho: "Todo pano tem um canto. O seu tem uma cantiga." Teste:
   locução curta e música gerada sobre imagens reais do produto.
3. **"Ficha técnica da vida"** (obviedade 5): etiqueta no formato de ficha de museu com um fato
   real sobre manchas, usos ou memórias; o cliente conta a história do seu pano. Gancho: "Pano novo é
   promessa. Pano usado é história." Teste: série de 6 cartões estilo ficha de museu.

Recomendação provisória: apostar no 3 (menos óbvio, depende de clientes reais, gera prova
social). O 1 é o mais fácil de executar e o 2 o mais emocional.

**Dados que faltam para fechar o plano multicanal**
1. O que vende e a faixa de preço.
2. Quem compra (casa, presente, revenda).
3. Onde vende hoje (loja física, site, Instagram, WhatsApp).
4. Verba mensal aproximada.
5. @ do Instagram ou site, para o agente ler sozinho.

---

## 9. Pendências e próximos passos

- [ ] Responder os 5 dados da Canto de Pano e gerar o plano multicanal completo.
- [ ] Decidir sobre abrir PR da branch `ccr-2be0a9a0-fnjfcb`.
- [ ] Decidir sobre a varredura só de leitura (Drive, Gmail, Todoist, memórias, Canva, Vercel)
      para localizar material da empresa anterior; nada será apagado sem aprovação item por item.
- [ ] Desinstalar manualmente, nas configurações do Claude, as skills da empresa anterior que
      ainda aparecem na conta (o agente não consegue removê-las).
- [ ] Renomear o repositório em GitHub → Settings → Rename, para tirar o nome antigo.
- [ ] Opcional: mover o agente para um repositório novo e vazio (o usuário cria, o Claude adiciona
      à sessão).
- [ ] Antes de gerar qualquer vídeo: confirmar créditos e modelo no ElevenLabs.

---

## 10. Como montar o Projeto no Claude

1. Em claude.ai, criar um Projeto novo (por exemplo "Agência Criativa IA").
2. Anexar como conhecimento: este `PROJECT.md`, `prompts/CREATIVE-PREMISE.md`,
   `prompts/PLAYBOOK.md` e os dois arquivos de `prompts/templates/`.
3. Em "instruções do projeto", colar o bloco abaixo.

```
Você é uma agência criativa em um só agente, com os papéis: atendimento, estratégia, direção
criativa, redação, direção de arte, produção de vídeo e produtora. Responda em português.

Premissa inegociável: ideias não óbvias, criatividade com inteligência, criatividade assistida
por IA. Siga o método do arquivo CREATIVE-PREMISE.md (lista do óbvio, banir, insight, rotas
forçadas, ataque, nota de obviedade, checagem de inteligência, protótipo com IA). Entregue 3
conceitos que sobreviveram, cada um em cartão, e diga o que foi descartado.

Regras: use só informações de marca que eu fornecer; não invente fatos, números ou
depoimentos; peça no máximo 3 perguntas e só se bloquearem o trabalho; não gaste créditos de
ferramentas sem meu OK e uma estimativa; prompts de vídeo em inglês, com formato e duração.
Nunca mencione, sugira ou use qualquer coisa da empresa anterior da qual não faço mais parte.
```

---

## 11. Ferramentas e serviços citados

ElevenLabs (imagem, vídeo, voz, música), Veo 3.1, Seedance 2.x, Kling 3, Studio do ElevenLabs,
CapCut, Descript, Claude Code (subagente), GitHub, Mem0, Vertiso Memory, Mem, Gryz, Firecrawl.
