# Vitrio
Site estático em português, sem dependências de execução. Sirva a pasta `dist` em qualquer hospedagem com suporte a diretórios e index.html.

## Ferramentas
- Imagens: Canvas, proporções predefinidas, conter/recortar, fundo, JPG/PNG/WebP, download. Limite: 20 MB e 40 MP.
- Margem: lucro, margem e preço-alvo com taxas percentuais e custos fixos por venda.
- UTM: URL API, preserva parâmetros, substitui UTM e copia o resultado.

## Desenvolvimento
Edite dist/app.js e dist/style.css. Rode `node --check dist/app.js` e `node prerender.cjs` após alterações no conteúdo. O prerender incorpora o HTML inicial para leitura por mecanismos de busca. Altere a constante base no prerender ao usar um domínio próprio. As páginas individuais preservam seus títulos e descrições.

## Publicação e monetização
A implantação inicial é privada. Para atrair visitantes e ser rastreado, o proprietário deve tornar o site público nas configurações do Sites. Pode conectar domínio próprio depois.

O AdSense está preparado no código, mas desativado (`enabled: false` em `dist/ads-config.js`). O site não carrega o script publicitário enquanto a opção permanece desligada. A configuração contém um publisher ID e `dist/ads.txt` está publicado; confira no painel se o ID corresponde à sua conta e se o site está aprovado.

Antes de ativar:

1. Adicione o site no AdSense e solicite a revisão. O Google só libera anúncios quando o status do site estiver como **Pronto**.
2. Ative Anúncios automáticos no painel do AdSense ou, para blocos manuais, crie as unidades e preencha os IDs em `slots.home` e `slots.tool`.
3. Configure as mensagens de consentimento aplicáveis ao seu público. Para anúncios personalizados no EEE, Reino Unido e Suíça, o Google exige uma CMP certificada integrada ao TCF.
4. Revise a política de privacidade e informe um canal de contato real.
5. Só então altere `enabled` para `true` e publique.

## Verificação
`node --check dist/app.js`. Navegação e cálculo inicial conferidos no navegador. Exportação de imagens exige arquivo real e navegador com suporte a Canvas; os formatos não suportados podem retornar PNG, cuja extensão é detectada na exportação.

## Melhorias da segunda versão
- Arrastar e soltar imagens, dimensões personalizadas de 1 a 4096 pixels e qualidade de exportação configurável.
- Mensagem com tamanho e formato do arquivo exportado; proteção contra carregamentos concorrentes.
- Gerador UTM bloqueia cópia de resultado antigo após alterações e rejeita campos obrigatórios vazios.
- Botão para restaurar exemplo da calculadora e atalho acessível para conteúdo.
- Metadados sem duplicação em reconstruções, dados estruturados WebSite e animação sutil com respeito a movimento reduzido.

Verificação: download real de WebP 800 × 600 confirmado com Pillow; alteração de UTM desabilita copiar; restauração da calculadora retorna lucro R$ 30 e margem 30%; sintaxe JavaScript e unicidade de canonical/dados estruturados conferidas.

## Expansão do catálogo
Seis páginas adicionadas: porcentagem (5 modos), desconto sucessivo, contador Unicode de texto, formatador/validador JSON com exportação, senhas com Web Crypto e link de WhatsApp. Busca local na home sem rastreamento. Total: 9 ferramentas.

Testes manuais: porcentagem 15% de 200 = 30; divisão por zero tratada; desconto de 20% + 10% em R$ 200 = R$ 144; texto de 4 palavras e 2 parágrafos contado corretamente; JSON válido e inválido; geração de senha; URL WhatsApp com mensagem Unicode; filtro da home. Sitemap contém 13 páginas.

Demanda: pesquisa pública identificou categorias recorrentes em portais de ferramentas; nenhum volume mensal foi medido ou inventado. Comparar termos no Planejador de Palavras-chave com Brasil/português para priorização quantitativa.

## Expansão para 14 ferramentas
Adicionadas calculadora de idade (anos completos e dias), diferença entre datas e soma de dias, conversor de unidades (5 grandezas), regra de três direta/inversa e Base64 UTF-8. Cada ferramenta possui URL, descrição, guia e processamento local. Sitemap: 18 páginas.

Verificação no navegador: regra direta 3/15/5 = 25 e inversa 3/10/5 = 6; 100 °C = 212 °F; nascimento em 29/02/2000 com referências 28/02/2025 e 01/03/2025; diferença de dois dias entre 28/02/2024 e 01/03/2024; subtração de dia; ida e volta de Base64 com “Olá 🌿”. A idade usa 1º de março como aniversário em anos não bissextos, explicitado na página. Dias são corridos, sem calendário de feriados.

## Deploy na Vercel
Importe LucasVentura52/vitrio-tools e mantenha a raiz do repositório como Root Directory. O vercel.json define framework Other, build com node prerender.cjs e saída dist. Não há dependências a instalar.

Configure SITE_URL com a origem definitiva do site (https://seu-dominio.com, sem caminho) e execute um novo deploy. Essa variável ajusta canonical, dados estruturados, robots.txt e sitemap.xml; sem ela o domínio inicial do Sites é preservado.

Após conectar o repositório à Vercel, os commits na branch de produção podem gerar deploys pela integração Git da Vercel. As futuras alterações devem preservar o histórico e partir do HEAD atual da branch.


## Ferramentas adicionadas
- Conversor de cores HEX, RGB e HSL com seletor e prévia.
- Analisador de URL para protocolo, domínio, caminho e parâmetros.
- Simulador de juros compostos com aportes mensais, prazo e aviso de que não considera tributos ou inflação.
- Conversor de JSON para CSV, com escaping e arquivo UTF-8 para planilhas.

As quatro ferramentas processam os dados localmente. Novas rotas: /conversor-cores/, /analisador-url/, /juros-compostos/ e /json-csv/.


## Gerador de QR Code
Gera QR Codes de texto e URLs no navegador, com tamanhos de 200 a 800 px, seleção de cores, prévia e download em PNG. A biblioteca QRCode.js é incluída localmente no site; o conteúdo digitado fica no navegador. Teste escanear o resultado antes de imprimir ou distribuir.


## Central de geradores para desenvolvimento
A rota /geradores-teste/ oferece 16 tipos de dados sintéticos: CPF e CNPJ com dígitos verificadores, números de cartão somente para teste Luhn, senha, RG/CNH/título/inscrição/certidão marcados como fictícios, nomes, empresa fictícia, nick, número, placa de teste, Lorem Ipsum e símbolos. Geração local via Web Crypto. Quantidade limitada a 20 por operação. Os identificadores oficiais são explicitamente para testes e não devem ser usados em cadastros ou transações reais.


## SEO de CPF e CNPJ de teste
As rotas /gerador-cpf/ e /gerador-cnpj/ têm title, descrição e conteúdo próprios para buscas de desenvolvedores. Ambas explicam que os identificadores são dados sintéticos de teste, sem consulta oficial. As rotas também entram no sitemap via prerender.


## Integração técnica do AdSense
A página de configuração fica em `dist/ads-config.js`. Quando `enabled` está desligado, nenhum script publicitário é carregado. Quando estiver ligado com um ID válido, o prerender inclui o código do AdSense no `<head>` de todas as páginas; `dist/ads.js` reaproveita esse carregador e cria blocos manuais quando `slots.home` ou `slots.tool` contêm IDs numéricos. Anúncios automáticos não precisam desses IDs de bloco.

A aprovação do site, a ativação de Anúncios automáticos e a CMP são configuradas na conta do AdSense; o repositório não consegue confirmar esses estados.
## Ferramentas adicionais
- Calculadora de IMC para adultos, com faixas de referência e orientação informativa.
- Gerador de slug para URLs com remoção de acentos e separadores configuráveis.
- Gerador de meta tags SEO com prévia, validação de URL e cópia do HTML.

Rotas: `/calculadora-imc/`, `/gerador-de-slug/` e `/gerador-meta-tags/`. O catálogo agora reúne 32 ferramentas e mantém a busca e a paginação visual em ordem alfabética.
