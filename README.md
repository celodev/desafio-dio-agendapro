# AgendaPro

> Mais organização, menos horários perdidos.

O **AgendaPro** é um MVP de agendamento para profissionais autônomos e pequenos estabelecimentos que trabalham com hora marcada. A solução começa pelos segmentos de beleza e estética e permite divulgar serviços, receber solicitações de horário e acompanhar os atendimentos em um painel administrativo.

## Demonstração

| Recurso | Endereço |
|---|---|
| Aplicação publicada | `https://desafio-dio-agendapro.lovable.app` |
| Repositório | `https://github.com/celodev/desafio-dio-agendapro` |

## Visão geral

Muitos profissionais organizam a agenda exclusivamente pelo WhatsApp. Embora o aplicativo seja importante para o relacionamento com clientes, depender apenas de conversas pode gerar solicitações incompletas, demora para encontrar horários, conflitos de agenda e dificuldade para acompanhar confirmações e cancelamentos.

O AgendaPro organiza esse processo em um fluxo simples:

1. o cliente consulta os serviços;
2. escolhe uma data e um horário disponível;
3. informa seus dados e revisa a solicitação;
4. o pedido é registrado como pendente;
5. o profissional acompanha e confirma o atendimento pelo painel;
6. o WhatsApp permanece disponível como canal complementar.

## Problema

Profissionais autônomos normalmente precisam executar o serviço, atender clientes e administrar o negócio ao mesmo tempo. No agendamento manual, isso pode causar:

- longas trocas de mensagens;
- perda de informações importantes;
- horários duplicados;
- dificuldade para visualizar os próximos atendimentos;
- demora na resposta ao cliente;
- perda de oportunidades comerciais.

## Solução

O AgendaPro oferece:

- página pública do profissional;
- catálogo de serviços;
- solicitação de horário em etapas;
- cálculo de disponibilidade;
- prevenção de conflitos de agenda;
- painel administrativo protegido;
- controle do status dos atendimentos;
- integração com o WhatsApp por link com mensagem preenchida.

## Público-alvo

O público inicial é formado por:

- manicures e pedicures;
- barbeiros;
- cabeleireiros;
- designers de sobrancelhas;
- esteticistas;
- massoterapeutas;
- salões de beleza e barbearias de pequeno porte;
- outros profissionais autônomos que trabalham com hora marcada.

A estratégia é validar primeiro com profissionais da beleza e estética. A expansão para outros segmentos será considerada após os testes do MVP.

## Proposta de valor

### Para o profissional

- reduzir mensagens repetitivas;
- organizar solicitações e atendimentos;
- divulgar serviços de forma profissional;
- diminuir conflitos de horário;
- manter o WhatsApp como canal de relacionamento.

### Para o cliente

- consultar serviços com facilidade;
- visualizar horários disponíveis;
- solicitar atendimento em poucos passos;
- revisar os dados antes do envio;
- continuar a conversa pelo WhatsApp quando necessário.

## Tese do MVP

> Profissionais autônomos e pequenos estabelecimentos da área de beleza e estética adotarão uma página de agendamento simples se ela reduzir as trocas de mensagens no WhatsApp, evitar solicitações incompletas e centralizar os próximos atendimentos.

## Hipóteses de validação

1. O profissional percebe valor em divulgar uma página própria de agendamento.
2. O cliente consegue solicitar um horário sem ajuda.
3. A seleção prévia de serviço, data e horário reduz mensagens repetitivas.
4. O painel facilita o acompanhamento das solicitações.
5. O link para o WhatsApp atende à comunicação complementar do primeiro MVP.
6. Profissionais do público inicial demonstram interesse em usar ou contratar a solução.

## Metas iniciais de validação

- entrevistar pelo menos 5 profissionais;
- realizar de 3 a 5 sessões de teste com o público-alvo;
- obter pelo menos 10 testes completos do fluxo público;
- registrar pelo menos 5 solicitações de agendamento;
- identificar os principais pontos de abandono;
- obter pelo menos uma manifestação real de interesse comercial.

Essas metas são indicadores do experimento e não representam validação definitiva do mercado.

## Escopo do MVP

O MVP é **single-tenant** e **single-professional**: representa um único negócio, uma única agenda e um único administrador por instalação.

### Área pública

- landing page;
- perfil do profissional;
- catálogo de serviços ativos;
- seleção de serviço, data e horário;
- formulário de identificação;
- revisão da solicitação;
- confirmação visual do envio;
- botão para continuar no WhatsApp;
- páginas iniciais de privacidade e termos de uso.

### Painel administrativo

- autenticação do administrador;
- visão geral dos atendimentos;
- lista e filtros de agendamentos;
- detalhes do agendamento;
- alteração de status;
- cadastro e edição de serviços;
- configuração de disponibilidade;
- bloqueio de datas e horários;
- lista simples de clientes;
- edição do perfil público.

## Fluxos principais

### Cliente

1. Acessa a página pública.
2. Consulta os serviços ativos.
3. Seleciona um serviço.
4. Escolhe uma data futura.
5. Seleciona um horário disponível.
6. Informa os dados de contato.
7. Revisa e envia a solicitação.
8. Visualiza o resumo e o status pendente.
9. Continua pelo WhatsApp, se desejar.

### Profissional

1. Entra no painel administrativo.
2. Consulta as solicitações pendentes.
3. Abre os detalhes do atendimento.
4. Confirma, conclui ou cancela o agendamento.
5. Entra em contato pelo WhatsApp quando necessário.
6. Cadastra serviços e ajusta a disponibilidade.

## Regras de negócio

- somente serviços ativos aparecem na área pública;
- somente datas futuras podem ser selecionadas;
- a duração do serviço determina o horário final;
- a grade de início dos horários usa o intervalo configurado;
- horários bloqueados não são oferecidos;
- solicitações `pending` e `confirmed` ocupam o intervalo;
- registros `completed` e `cancelled` permanecem no histórico, mas não bloqueiam horários;
- o sistema não aceita dois agendamentos ativos sobrepostos;
- nome, telefone, serviço, data, horário e consentimento são obrigatórios;
- o preço do serviço é opcional;
- a solicitação pública começa com status `pending`;
- somente o profissional confirma o atendimento;
- as datas são exibidas em `dd/MM/yyyy` e as horas em `HH:mm`;
- o fuso horário adotado é `America/Bahia`.

A regra de sobreposição é:

```text
novo_inicio < existente_fim
e
novo_fim > existente_inicio
```

## Status dos agendamentos

| Status | Significado | Bloqueia o horário? |
|---|---|---:|
| `pending` | Solicitação aguardando análise | Sim |
| `confirmed` | Atendimento confirmado | Sim |
| `completed` | Atendimento concluído | Não |
| `cancelled` | Atendimento cancelado | Não |

## O que permanece manual

Para manter o MVP pequeno e validar a tese antes de automatizar processos, permanecem manuais:

- configuração inicial do profissional;
- confirmação final do horário;
- comunicação com o cliente;
- cobrança e pagamento;
- tratamento de exceções;
- suporte ao usuário;
- coleta e análise de feedback.

## Fora do escopo

Não fazem parte desta versão:

- pagamento integrado;
- assinatura recorrente;
- marketplace;
- múltiplas unidades;
- agendas para vários profissionais;
- sincronização com Google Calendar ou Outlook;
- mensagens automáticas por WhatsApp, SMS ou e-mail;
- chatbot e automações com n8n;
- avaliações, fidelidade e cupons;
- relatórios financeiros;
- aplicativo móvel nativo;
- recursos de inteligência artificial dentro da aplicação.

## Business Model Canvas

| Bloco | Definição inicial |
|---|---|
| Segmentos de clientes | Profissionais autônomos e pequenos estabelecimentos de beleza e estética |
| Proposta de valor | Agendamento simples, organização da rotina e redução das trocas de mensagens |
| Canais | WhatsApp, Instagram, indicação, visitas locais e redes profissionais |
| Relacionamento | Configuração assistida, suporte direto e coleta de feedback |
| Fontes de receita | Assinatura mensal e serviço opcional de configuração |
| Recursos principais | Aplicação web, Lovable Cloud, WhatsApp, GitHub e conhecimento do público |
| Atividades principais | Desenvolvimento, configuração, suporte, captação e validação |
| Parcerias principais | Profissionais da beleza, salões, barbearias e divulgadores locais |
| Estrutura de custos | Construção, hospedagem, domínio, suporte e divulgação |

## Modelo de receita hipotético

Os valores abaixo são hipóteses para entrevistas e testes, não preços validados:

- plano gratuito: perfil e agendamento básico;
- plano profissional: de **R$ 19,90 a R$ 39,90 por mês**;
- configuração assistida: de **R$ 49,00 a R$ 99,00**, em cobrança única.

A disposição a pagar será validada com profissionais antes de qualquer definição comercial.

## Dimensionamento inicial de mercado

O dimensionamento definitivo dependerá de fontes oficiais e da delimitação geográfica.

- **TAM:** profissionais e pequenos estabelecimentos brasileiros que trabalham com agendamento.
- **SAM:** profissionais da beleza e estética nas regiões em que o AgendaPro consegue operar e prestar suporte inicialmente.
- **SOM:** parcela do SAM que pode ser alcançada nos primeiros 12 meses por contato direto, indicação e divulgação local.

Exemplo acadêmico, sem representar receita garantida:

- 50 clientes pagantes;
- mensalidade média de R$ 29,90;
- receita mensal estimada de R$ 1.495,00;
- receita anual estimada de R$ 17.940,00.

## Design Universal e acessibilidade

O AgendaPro foi planejado para proporcionar boa experiência ao maior número possível de usuários.

Requisitos principais:

- HTML semântico;
- navegação por teclado;
- foco visível;
- contraste compatível com WCAG 2.2 nível AA;
- campos com rótulos persistentes;
- mensagens de erro claras e associadas aos campos;
- textos alternativos para imagens;
- alvos de toque confortáveis;
- interface responsiva;
- status identificados por texto, não apenas por cor;
- respeito a `prefers-reduced-motion`;
- linguagem simples em português do Brasil.

## Privacidade e segurança

O MVP coleta somente os dados necessários para a solicitação de agendamento.

Cuidados previstos:

- consentimento explícito para contato;
- aviso inicial de privacidade;
- painel protegido por autenticação;
- validação no cliente e no backend;
- controle de acesso aos dados pessoais;
- prevenção de duplicidade e conflito;
- ausência de chaves, tokens e senhas no repositório;
- uso de variáveis de ambiente;
- remoção de dados pessoais dos logs;
- revisão de segurança antes da publicação.

Os textos de privacidade e termos do MVP são iniciais e não substituem revisão jurídica para operação comercial.

## Tecnologias

Tecnologias previstas, sujeitas à confirmação após a geração e exportação do código:

- Lovable;
- Lovable Cloud;
- React;
- TypeScript;
- Tailwind CSS;
- Git e GitHub.

## Estrutura esperada

```text
.
├── public/
├── src/
│   ├── components/
│   ├── hooks/
│   ├── lib/
│   ├── pages/
│   └── types/
├── .env.example
├── .gitignore
├── MEGA_PROMPT.md
├── MATRIZ_REQUISITOS.md
├── README.md
└── package.json
```

A estrutura deve ser atualizada após a exportação. Nenhum arquivo inexistente deve ser mencionado na versão final do README.

## Como executar localmente

### Pré-requisitos

- Node.js em versão compatível com o projeto;
- npm;
- Git.

### Instalação

```bash
git clone https://github.com/celodev/desafio-dio-agendapro.git
cd desafio-dio-agendapro
npm install
```

### Configuração

1. Copie o arquivo de exemplo:

```bash
cp .env.example .env
```

2. Preencha somente as variáveis exigidas pelo projeto.
3. Nunca versione o arquivo `.env`.

### Execução

```bash
npm run dev
```

Abra o endereço exibido pelo servidor de desenvolvimento.

### Build de produção

```bash
npm run build
```

## Variáveis de ambiente

Liste aqui somente os nomes das variáveis realmente utilizadas, sem valores secretos.

```env
VITE_BACKEND_URL=
VITE_PUBLIC_KEY=
```

## Documentação

| Documento | Finalidade |
|---|---|
| ./MEGA_PROMPT.md | Escopo e instruções usados na construção do MVP |
| ./MATRIZ_REQUISITOS.md | Requisitos funcionais, não funcionais e critérios de aceite |
| ./README.md | Visão geral, execução, validação e evidências do projeto |

## Requisitos e critérios de aceite

A matriz detalhada está disponível em ./MATRIZ_REQUISITOS.md. Ela contém:

- 27 requisitos funcionais;
- 18 requisitos não funcionais;
- 10 regras de negócio rastreáveis;
- prioridades P0 e P1;
- evidências esperadas;
- critérios de saída do MVP.

O MVP só será considerado pronto quando:

- [ ] todos os requisitos P0 forem aprovados;
- [ ] não houver conflito em testes sequenciais ou concorrentes;
- [ ] o painel não puder ser acessado sem autenticação;
- [ ] o fluxo funcionar em uma tela de 360 px sem rolagem horizontal;
- [ ] não houver erros não tratados no console;
- [ ] a revisão de segurança do Lovable for executada;
- [ ] nenhum segredo estiver presente no repositório;
- [ ] a aplicação abrir pela URL pública em uma janela anônima;
- [ ] o README contiver URLs e evidências reais.

## Plano de testes

### Fluxo principal

- [ ] Abrir a aplicação pela URL pública.
- [ ] Consultar os serviços ativos.
- [ ] Selecionar serviço, data e horário.
- [ ] Enviar uma solicitação válida.
- [ ] Visualizar a confirmação da solicitação.
- [ ] Abrir a mensagem preenchida no WhatsApp.
- [ ] Localizar o agendamento no painel.
- [ ] Alterar o status para `confirmed`.

### Validações

- [ ] Impedir envio de formulário incompleto.
- [ ] Impedir seleção de data passada.
- [ ] Ocultar horários bloqueados.
- [ ] Impedir conflito de horário.
- [ ] Tratar um horário ocupado durante o envio.
- [ ] Não exibir serviço inativo.
- [ ] Solicitar confirmação antes de cancelar.

### Responsividade e acessibilidade

- [ ] Testar nas larguras de 360 px, 768 px e 1280 px.
- [ ] Confirmar ausência de rolagem horizontal.
- [ ] Navegar usando apenas o teclado.
- [ ] Verificar foco visível.
- [ ] Revisar contraste com Lighthouse ou axe DevTools.
- [ ] Verificar rótulos e mensagens de erro.

### Segurança

- [ ] Executar a revisão de segurança do Lovable.
- [ ] Verificar as regras de acesso do backend.
- [ ] Confirmar que as rotas `/admin/*` exigem autenticação.
- [ ] Procurar chaves, tokens e senhas no repositório.
- [ ] Remover logs com dados pessoais.
- [ ] Testar a aplicação em janela anônima.

## Evidências da aplicação

Adicione imagens reais após a construção do projeto:

| Tela | Evidência |
|---|---|
| Landing page | `docs/screenshots/landing-page.png` |
| Perfil público | `docs/screenshots/perfil-publico.png` |
| Seleção de horário | `docs/screenshots/agendamento.png` |
| Confirmação | `docs/screenshots/confirmacao.png` |
| Painel administrativo | `docs/screenshots/painel.png` |
| Gestão de serviços | `docs/screenshots/servicos.png` |

## Registro de correções

Documente somente correções realmente solicitadas e executadas no Lovable.

| Data | Problema observado | Correção solicitada | Resultado |
|---|---|---|---|
| 2026-11-16 | Início do planejamento da Fase 2 | Modularização de templates e leads | Planejamento aprovado |
| 2026-11-17 | Revisão econômica e de segurança | Separação de leads, controle de cartão e IA | Documentação atualizada |
| 2026-11-18 | Consolidação da documentação | Unificação do PRD e remoção de duplicidades | README e artefatos integrados |

## Estratégia de construção

Para reduzir o consumo de créditos no Lovable:

1. revisar o escopo antes da construção;
2. executar primeiro o modo de planejamento;
3. enviar o mega prompt em uma única mensagem;
4. não gerar imagens ou vídeos por IA;
5. testar toda a aplicação antes de solicitar alterações;
6. consolidar os problemas em um único prompt de correção;
7. não adicionar funcionalidades fora do MVP;
8. monitorar o consumo de construção e execução.

## Possíveis evoluções

- confirmação e lembretes automáticos;
- integração com Google Calendar e Outlook;
- planos e cobrança recorrente;
- pagamento antecipado;
- agenda para múltiplos profissionais;
- múltiplas unidades e salas;
- relatórios de ocupação;
- lista de espera;
- política configurável de cancelamento;
- domínio personalizado;
- aplicativo móvel;
- expansão para saúde, consultoria, manutenção e outros serviços com hora marcada.

## Projeto técnico e apresentação comercial

Este repositório documenta o projeto acadêmico e técnico: problema, hipóteses, escopo, requisitos, desenvolvimento, testes, publicação e evidências.

A apresentação comercial do AgendaPro deve ser mantida separadamente. Ela será voltada a benefícios, demonstração, planos, implantação e contratação, sem substituir a documentação técnica deste repositório.

---

# 🚀 Evolução Incremental do Projeto — Fase 2 e Atualizações

> As seções abaixo documentam a evolução arquitetural e funcional adicionada incrementalmente ao MVP original, mantendo a compatibilidade estrita com todos os agendamentos, serviços e regras existentes.

---

## 1. Escopo Funcional da Fase 2

A Fase 2 expande o AgendaPro sem quebrar o fluxo de agendamento funcional já aprovado.

### 1.1 Perfil Personalizado do Parceiro
O profissional ganha controle total sobre a apresentação visual e comercial do seu negócio:
- **Identidade de marca:** nome do negócio, responsável, segmento, descrição, proposta de valor e chamada para ação (CTA).
- **Mídia:** logo, foto de capa e galeria com até **6 imagens** de até **3 MB** cada (JPG, JPEG, PNG, WebP).
- **Cores acessíveis:** configuração de cor primária, secundária e destaque, respeitando contraste WCAG 2.2 AA.
- **Contatos comerciais:** WhatsApp com mensagem preenchida, telefone, e-mail, Instagram, cidade e endereço opcional.
- **URL pública personalizada:** rota pública no padrão `/p/:slug`, com validação de unicidade, caracteres permitidos e estados de rascunho, prévia, publicado e despublicado.
- **Link público integrado:** bloco em *Perfil e marca* com botão de cópia de link, abertura de perfil em nova aba (`noopener noreferrer`) e aviso claro para perfis em rascunho ou despublicados.

### 1.2 Sistema de Templates Reutilizáveis por Segmento
Em vez de duplicar componentes ou páginas, o AgendaPro adota um motor unificado de templates configurados por `template_key`:

| Chave Interna | Nome Visível (PT) | Segmento Alvo | Paleta Padrão |
|---|---|---|---|
| `beauty-soft` | **Beleza Suave** | Manicures, estética, sobrancelhas e salões | Violeta `#7C3AED`, rosa `#EC4899`, fundo `#FDF8FF` |
| `barber-classic` | **Barbearia Clássica** | Barbearias e cabeleireiros | Grafite `#1F2937`, dourado `#D4A017`, fundo `#F9FAFB` |
| `wellness-clean` | **Bem-estar Essencial** | Massoterapia, terapias e bem-estar | Verde-petróleo `#0F766E`, verde `#65A30D`, fundo `#F8FAF9` |
| `professional-neutral` | **Profissional Moderno** | Consultores, técnicos e autônomos | Azul `#2563EB`, verde `#0F766E`, fundo `#F8FAFC` |

- **Preservação de dados:** a troca de template altera composição visual, tipografia e espaçamentos, mas **nunca apaga dados cadastrados**.
- **Ação rápida:** botão *Restaurar cores do template* permite voltar à harmonia cromática original a qualquer momento.

### 1.3 Gestão de Leads com Deduplicação
- **Captura:** formulário público de interesse e fluxo de agendamento geram registros na entidade `leads`.
- **Deduplicação automática:** normalização do telefone (remoção de caracteres não numéricos) garantindo a chave lógica `partner_id + phone_normalized`.
- **Isolamento:** o mesmo número de telefone pode existir em parceiros diferentes sem cruzamento de dados.
- **Status do lead:** `new` → `contacted` → `qualified` → `converted` / `lost`.
- **Origens rastreadas:** `public_profile`, `booking`, `whatsapp` e `manual`.

### 1.4 Clientes e Validação Manual de Pagamento
Ao receber um formulário qualificado (nome, telefone válido, interesse/serviço e consentimento):
1. Cria/atualiza o lead e o cliente correspondente.
2. Define `customer_status = pending_validation` e `payment_status = pending`.
3. Exibe o cliente na aba administrativa **Pendentes de validação**.
4. **Governança rígida:** a aprovação do cliente como `active` é **bloqueada** até que o pagamento seja conferido manualmente como `paid` ou autorizado como `waived` (dispensado).
5. Nenhum pagamento muda de status automaticamente.

### 1.5 Formas de Pagamento Seguras (Sem Armazenamento de Cartão)
- **Pix Manual:** exibe chave configurada pelo parceiro (CPF/CNPJ, e-mail, telefone ou aleatória), nome do recebedor, valor e botão copiar. Chave mascarada no painel administrativo fora do modo de edição.
- **Cartão por Link Externo:** o botão de pagamento direciona para uma URL externa segura fornecida pelo parceiro. O AgendaPro **não coleta nem armazena número de cartão, validade ou CVV**. Validação de HTTPS obrigatória no servidor.
- **Outras opções:** dinheiro (`cash`) e transferência bancária (`bank_transfer`) com instruções customizadas.

### 1.6 Assistente de Perfil com Inteligência Artificial
Integrado na seção *Perfil e marca*, gera sugestões personalizadas de headline, descrições, proposta de valor, mensagem de WhatsApp e recomendação de template a partir dos dados do negócio informados pelo parceiro:
- **Papel de copiloto:** todo o conteúdo gerado pela IA é apresentado como rascunho/sugestão para revisão e edição humana.
- **Proibição de alucinação:** a IA é instruída estritamente a não inventar preços, contatos, endereços ou certificações.
- **Publicação segura:** a IA nunca publica um perfil por conta própria.

---

## 2. Modelo de Dados Unificado (Schemas e Entidades)

O banco de dados foi expandido com migrações puramente aditivas e segregação estrita por `partner_id`:

```text
partner_profiles
├── id, owner_user_id, business_name, professional_name, segment
├── headline, short_description, description, value_proposition, call_to_action
├── logo_url, logo_alt, cover_url, cover_alt, gallery_urls
├── primary_color, secondary_color, accent_color
├── whatsapp, phone, email, instagram, city, address_optional
├── template_key, profile_slug, is_published, created_at, updated_at

leads
├── id, partner_id, full_name, phone_normalized, email_optional
├── source, lead_type (customer | platform_partner), interest, notes_optional
├── consent_to_contact, consent_at, lead_status, created_at, updated_at

customers
├── id, partner_id, lead_id_optional, full_name, phone_normalized, email_optional
├── customer_status (pending_validation | active | inactive | rejected)
├── rejection_reason_optional, validated_at_optional, validated_by_optional
├── created_at, updated_at

payment_settings
├── id, partner_id, pix_enabled, pix_key_type, pix_key_encrypted
├── pix_receiver_name, pix_receiver_city, card_link_enabled, card_payment_url
├── cash_enabled, bank_transfer_enabled, payment_instructions, default_due_days
├── created_at, updated_at

payments
├── id, partner_id, customer_id, payment_method, payment_status, payment_purpose
├── payment_amount, payment_due_date, payment_reference, payment_proof_url_optional
├── client_reported_paid_at_optional, paid_at_optional, validated_at_optional, validated_by_optional
├── created_at, updated_at

ai_profile_generations
├── id, partner_id, version, input_data, output_data, accepted_fields, generation_status
├── created_at, updated_at
```

---

## 3. Arquitetura Comercial e Planos (Fase 3)

Configuração centralizada de planos (`plans.ts` / tabela `plans`) com página pública informativa em `/planos`:

| Plano | Mensalidade | Anualidade | Profissionais | Recursos Principais |
|---|---|---|---|---|
| **Básico** | R$ 29,90 | R$ 305,00 | 1 ativo | 1 agenda, template Profissional Moderno, até 5 serviços, 80 agendamentos/mês, Pix manual. *(Adicional futuro: R$ 19,90/mês, máx 2)* |
| **Profissional** ⭐ | R$ 59,90 | R$ 611,00 | Até 3 (Em breve) | Todos os 4 templates, galeria com até 6 fotos, cores personalizadas, 20 serviços, 500 agendamentos/mês, Pix + cartão por link, 1 geração IA + 2 regenerações. *(Adicional futuro: R$ 19,90/mês, máx 5)* |
| **Premium** | R$ 99,90 | R$ 1.019,00 | Até 5 (Em breve) | Galeria de até 12 fotos, até 30 serviços, política de uso justo para agendamentos e leads, 5 gerações de perfil IA/mês, histórico detalhado de pagamentos. *(Adicional futuro: R$ 14,90/mês, máx 10)* |

- **Período de testes:** 7 dias gratuitos no plano Profissional para novas contas, sem exigência de cartão.
- **Transição suave:** parceiros existentes recebem 30 dias de transição no plano Profissional sem bloqueio retroativo.
- **Separação de leads operacionais e comerciais:**
  - `lead_type = customer` → cliente de manicure/barbearia do parceiro.
  - `lead_type = platform_partner` → interessado em contratar a plataforma AgendaPro.
  - *Garantia:* pagamento de serviço de manicure **jamais** ativa uma conta de parceiro no sistema.

---

## 4. Guia de Implementação no Lovable

Para orientar manutenções e novas entregas com eficiência máxima de créditos:
- **Modo Plan:** todo desenvolvimento no Lovable deve começar obrigatoriamente no modo de planejamento com auditoria dos arquivos afetados.
- **Versão de Prompt Econômico (até 5 créditos):** para sessões com restrição de saldo, o arquivo de apoio `MEGA_PROMPT_LOVABLE_AgendaPro.md` contém um bloco pronto que executa apenas os 4 ajustes visuais essenciais (imagens 3 MB, templates em PT, link público e página `/planos` informativa) sem alterações no banco de dados.

---

## Status do Projeto

**Fase 1 (MVP de agendamento):** Concluído e operacional.  
**Fase 2 (Perfis, templates, leads, pagamentos e IA):** Documentação consolidada e homologada para execução incremental.

## Autor

**Marcelo dos Santos Almeida**

## Licença

Projeto desenvolvido no âmbito do Desafio da DIO (Digital Innovation One).
