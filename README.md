# AgendaPro

> Mais organização, menos horários perdidos.

O **AgendaPro** é um MVP de agendamento para profissionais autônomos e pequenos estabelecimentos que trabalham com hora marcada. A solução começa pelos segmentos de beleza e estética e permite divulgar serviços, receber solicitações de horário e acompanhar os atendimentos em um painel administrativo.

## Demonstração

| Recurso | Endereço |
|---|---|
| Aplicação publicada | `https://pixel-perfect-replay-76778.lovable.app` |
| Repositório | `[https://github.com/celodev/desafio-dio-agendapro]` |

> Antes da entrega, substitua os endereços acima e remova este aviso.

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

> Antes da publicação final, mantenha nesta lista somente as tecnologias realmente presentes no repositório.

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

> Valide estes comandos no projeto exportado antes da publicação.

### Pré-requisitos

- Node.js em versão compatível com o projeto;
- npm;
- Git.

### Instalação

```bash
git clone ADICIONAR_URL_DO_REPOSITORIO
cd agendapro
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

> Substitua esses nomes, se necessário, pelos identificadores existentes no código exportado.

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

> Crie a pasta `docs/screenshots/` somente quando houver capturas reais. Depois, substitua a tabela por imagens Markdown ou links para os arquivos.

## Registro de correções

Documente somente correções realmente solicitadas e executadas no Lovable.

| Data | Problema observado | Correção solicitada | Resultado |
|---|---|---|---|
| A preencher | A preencher | A preencher | A preencher |

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

## Status

**Em planejamento.** O status deve ser alterado para **Em desenvolvimento** quando a construção no Lovable for iniciada e para **MVP publicado** somente depois da publicação e dos testes mínimos.

## Autor

**Marcelo dos Santos Almeida**

## Licença

A licença ainda não foi definida. Antes da publicação, escolha uma licença compatível com o objetivo do repositório e adicione o arquivo `LICENSE`.
