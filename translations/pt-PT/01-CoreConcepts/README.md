# Conceitos Fundamentais do MCP: Dominando o Protocolo de Contexto do Modelo para Integração de IA

[![Conceitos Fundamentais do MCP](../../../translated_images/pt-PT/02.8203e26c6fb5a797.webp)](https://youtu.be/earDzWGtE84)

_(Clique na imagem acima para ver o vídeo desta lição)_

O [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) é uma estrutura padronizada poderosa que otimiza a comunicação entre Grandes Modelos de Linguagem (LLMs) e ferramentas externas, aplicações e fontes de dados.  
Este guia conduzirá você através dos conceitos fundamentais do MCP. Irá aprender sobre a sua arquitetura cliente-servidor, componentes essenciais, mecânicas de comunicação e melhores práticas de implementação.

- **Consentimento Explícito do Utilizador**: Todo o acesso a dados e operações requer aprovação explícita do utilizador antes da execução. Os utilizadores devem compreender claramente quais os dados que serão acedidos e que ações serão executadas, com controlo granular sobre permissões e autorizações.

- **Proteção de Privacidade dos Dados**: Os dados do utilizador só são expostos com consentimento explícito e devem ser protegidos por controlos de acesso robustos durante todo o ciclo de vida da interação. As implementações devem prevenir a transmissão não autorizada de dados e manter limites rigorosos de privacidade.

- **Segurança na Execução de Ferramentas**: Cada invocação de ferramenta requer consentimento explícito do utilizador com compreensão clara da funcionalidade, parâmetros e impacto potencial da ferramenta. Limites de segurança robustos devem impedir execuções não intencionadas, inseguras ou maliciosas.

- **Segurança na Camada de Transporte**: Todos os canais de comunicação devem usar mecanismos adequados de encriptação e autenticação. Conexões remotas devem implementar protocolos de transporte seguros e gestão adequada de credenciais.

#### Diretrizes de Implementação:

- **Gestão de Permissões**: Implementar sistemas de permissão de granularidade fina que permitam aos utilizadores controlar quais servidores, ferramentas e recursos são acessíveis  
- **Autenticação & Autorização**: Usar métodos seguros de autenticação (OAuth, chaves API) com gestão adequada de tokens e expiração  
- **Validação de Entrada**: Validar todos os parâmetros e dados de entrada segundo esquemas definidos para prevenir ataques de injeção  
- **Registo de Auditoria**: Manter registos abrangentes de todas as operações para monitorização de segurança e conformidade

## Visão Geral

Esta lição explora a arquitetura fundamental e os componentes que compõem o ecossistema do Model Context Protocol (MCP). Irá aprender sobre a arquitetura cliente-servidor, os componentes-chave e os mecanismos de comunicação que suportam as interações MCP.

## Objetivos de Aprendizagem Principais

No final desta lição, você irá:

- Compreender a arquitetura cliente-servidor do MCP.  
- Identificar papéis e responsabilidades dos Hosts, Clientes e Servidores.  
- Analisar as funcionalidades centrais que tornam o MCP uma camada de integração flexível.  
- Aprender como a informação flui dentro do ecossistema MCP.  
- Obter insights práticos através de exemplos de código em .NET, Java, Python e JavaScript.

## Arquitetura MCP: Um Olhar Mais Profundo

O ecossistema MCP é construído sobre um modelo cliente-servidor. Esta estrutura modular permite que aplicações de IA interajam eficientemente com ferramentas, bases de dados, APIs e recursos contextuais. Vamos detalhar esta arquitetura nos seus componentes principais.

No seu centro, o MCP segue uma arquitetura cliente-servidor onde uma aplicação host pode conectar-se a múltiplos servidores:

```mermaid
flowchart LR
    subgraph "O Seu Computador"
        Host["Anfitrião com MCP (Visual Studio, VS Code, IDEs, Ferramentas)"]
        S1["Servidor MCP A"]
        S2["Servidor MCP B"]
        S3["Servidor MCP C"]
        Host <-->|"Protocolo MCP"| S1
        Host <-->|"Protocolo MCP"| S2
        Host <-->|"Protocolo MCP"| S3
        S1 <--> D1[("Fonte de Dados Local A")]
        S2 <--> D2[("Fonte de Dados Local B")]
    end
    subgraph "Internet"
        S3 <-->|"APIs Web"| D3[("Serviços Remotos")]
    end
```
- **Hosts MCP**: Programas como VSCode, Claude Desktop, IDEs ou ferramentas IA que querem aceder a dados via MCP  
- **Clientes MCP**: Clientes do protocolo que mantêm ligações 1:1 com servidores  
- **Servidores MCP**: Programas leves que expõem capacidades específicas através do Model Context Protocol padronizado  
- **Fontes de Dados Locais**: Os ficheiros, bases de dados e serviços do seu computador que os servidores MCP podem aceder de forma segura  
- **Serviços Remotos**: Sistemas externos disponíveis pela internet aos quais servidores MCP podem ligar-se via APIs.

O Protocolo MCP é um padrão em evolução usando versionamento baseado em datas (formato AAAA-MM-DD). A versão atual do protocolo é **2025-11-25**. Pode ver as atualizações mais recentes na [especificação do protocolo](https://modelcontextprotocol.io/specification/2025-11-25/)

### 1. Hosts

No Model Context Protocol (MCP), os **Hosts** são aplicações de IA que servem como a interface primária através da qual os utilizadores interagem com o protocolo. Os Hosts coordenam e gerem conexões para múltiplos servidores MCP criando clientes MCP dedicados para cada conexão ao servidor. Exemplos de Hosts incluem:

- **Aplicações de IA**: Claude Desktop, Visual Studio Code, Claude Code  
- **Ambientes de Desenvolvimento**: IDEs e editores de código com integração MCP  
- **Aplicações Personalizadas**: Agentes IA construídos para fins específicos e ferramentas

Os **Hosts** são aplicações que coordenam as interações com modelos de IA. Eles:

- **Orquestram Modelos de IA**: Executam ou interagem com LLMs para gerar respostas e coordenar fluxos de trabalho de IA  
- **Gerem Ligações de Cliente**: Criam e mantêm um cliente MCP por cada conexão ao servidor MCP  
- **Controlam a Interface do Utilizador**: Gerem o fluxo da conversa, interações do utilizador e apresentação de respostas  
- **Aplicam Segurança**: Controlam permissões, restrições de segurança e autenticação  
- **Gerem o Consentimento do Utilizador**: Administram a aprovação do utilizador para partilha de dados e execução de ferramentas

### 2. Clientes

Os **Clientes** são componentes essenciais que mantêm conexões dedicadas um-para-um entre Hosts e servidores MCP. Cada cliente MCP é instanciado pelo Host para conectar a um servidor MCP específico, garantindo canais de comunicação organizados e seguros. Múltiplos clientes permitem que Hosts conectem-se a vários servidores simultaneamente.

Os **Clientes** são componentes de ligação dentro da aplicação host. Eles:

- **Comunicação de Protocolo**: Enviam pedidos JSON-RPC 2.0 a servidores com prompts e instruções  
- **Negociação de Capacidades**: Negociam funcionalidades suportadas e versões do protocolo com servidores durante a inicialização  
- **Execução de Ferramentas**: Gerem os pedidos de execução de ferramentas dos modelos e processam as respostas  
- **Atualizações em Tempo Real**: Gerem notificações e atualizações em tempo real enviadas pelos servidores  
- **Processamento de Respostas**: Processam e formatam respostas do servidor para exibição aos utilizadores  

### 3. Servidores

Os **Servidores** são programas que fornecem contexto, ferramentas e capacidades aos clientes MCP. Podem executar localmente (na mesma máquina que o Host) ou remotamente (em plataformas externas), sendo responsáveis por tratar pedidos dos clientes e fornecer respostas estruturadas. Os servidores expõem funcionalidades específicas através do Model Context Protocol padronizado.

Os **Servidores** são serviços que fornecem contexto e capacidades. Eles:

- **Registo de Funcionalidades**: Registam e expõem primitivas disponíveis (recursos, prompts, ferramentas) aos clientes  
- **Processamento de Pedidos**: Recebem e executam chamadas de ferramentas, pedidos de recursos e prompts dos clientes  
- **Provisão de Contexto**: Fornecem informação contextual e dados para melhorar as respostas do modelo  
- **Gestão de Estado**: Mantêm o estado da sessão e tratam interações com estado, quando necessárias  
- **Notificações em Tempo Real**: Enviam notificações sobre mudanças de capacidades e atualizações para clientes ligados

Os servidores podem ser desenvolvidos por qualquer pessoa para estender as capacidades do modelo com funcionalidades especializadas, suportando cenários de implantação locais e remotos.

### 4. Primitivas do Servidor

No Model Context Protocol (MCP), os servidores fornecem três **primitivas** principais que definem os blocos fundamentais para interações ricas entre clientes, hosts e modelos de linguagem. Estas primitivas especificam os tipos de informação contextual e ações disponíveis através do protocolo.

Os servidores MCP podem expor qualquer combinação das três primitivas principais seguintes:

#### Recursos

Os **Recursos** são fontes de dados que fornecem informação contextual às aplicações de IA. Representam conteúdos estáticos ou dinâmicos que podem aprimorar a compreensão do modelo e a tomada de decisão:

- **Dados Contextuais**: Informação estruturada e contexto para consumo do modelo de IA  
- **Bases de Conhecimento**: Repositórios de documentos, artigos, manuais e artigos de investigação  
- **Fontes de Dados Locais**: Ficheiros, bases de dados e informação do sistema local  
- **Dados Externos**: Respostas de APIs, serviços web e dados de sistemas remotos  
- **Conteúdo Dinâmico**: Dados em tempo real atualizados conforme condições externas

Os recursos são identificados por URIs e suportam descoberta através dos métodos `resources/list` e recuperação mediante `resources/read`:

```text
file://documents/project-spec.md
database://production/users/schema
api://weather/current
```

#### Prompts

Os **Prompts** são modelos reutilizáveis que ajudam a estruturar interações com modelos de linguagem. Fornecem padrões padronizados de interação e fluxos de trabalho templados:

- **Interações Baseadas em Modelos**: Mensagens pré-estruturadas e iniciadores de conversação  
- **Modelos de Fluxos de Trabalho**: Sequências padronizadas para tarefas e interações comuns  
- **Exemplos Few-shot**: Modelos baseados em exemplos para instrução do modelo  
- **Prompts de Sistema**: Prompts fundamentais que definem o comportamento e contexto do modelo  
- **Modelos Dinâmicos**: Prompts parametrizados que se adaptam a contextos específicos

Os prompts suportam substituição de variáveis e podem ser descobertos via `prompts/list` e obtidos com `prompts/get`:

```markdown
Generate a {{task_type}} for {{product}} targeting {{audience}} with the following requirements: {{requirements}}
```

#### Ferramentas

As **Ferramentas** são funções executáveis que modelos IA podem invocar para realizar ações específicas. Representam os “verbos” do ecossistema MCP, permitindo que modelos interajam com sistemas externos:

- **Funções Executáveis**: Operações discretas que modelos podem invocar com parâmetros específicos  
- **Integração com Sistemas Externos**: Chamadas API, consultas a bases de dados, operações em ficheiros, cálculos  
- **Identidade Única**: Cada ferramenta tem um nome distinto, descrição e esquema de parâmetros  
- **E/S Estruturada**: As ferramentas aceitam parâmetros validados e retornam respostas estruturadas e tipadas  
- **Capacidades de Ação**: Permitem que modelos realizem ações no mundo real e obtenham dados em tempo real

Ferramentas são definidas com JSON Schema para validação de parâmetros, descobertas via `tools/list` e executadas por `tools/call`. As ferramentas podem também incluir **ícones** como metadados adicionais para melhor apresentação na interface de utilizador.

**Anotações de Ferramentas**: Ferramentas suportam anotações comportamentais (ex.: `readOnlyHint`, `destructiveHint`) que descrevem se uma ferramenta é só leitura ou destrutiva, ajudando os clientes a tomar decisões informadas sobre a execução da ferramenta.

Exemplo de definição de ferramenta:

```typescript
server.tool(
  "search_products", 
  {
    query: z.string().describe("Search query for products"),
    category: z.string().optional().describe("Product category filter"),
    max_results: z.number().default(10).describe("Maximum results to return")
  }, 
  async (params) => {
    // Executar pesquisa e devolver resultados estruturados
    return await productService.search(params);
  }
);
```

## Primitivas do Cliente

No Model Context Protocol (MCP), os **clientes** podem expor primitivas que permitem aos servidores solicitar capacidades adicionais à aplicação host. Estas primitivas do lado do cliente possibilitam implementações de servidor mais ricas e interativas que podem aceder a capacidades do modelo IA e interações do utilizador.

### Amostragem

A **Amostragem** permite que servidores solicitem conclusões do modelo de linguagem a partir da aplicação IA do cliente. Esta primitiva permite que servidores acedam às capacidades do LLM sem embutir as suas próprias dependências de modelo:

- **Acesso Independente do Modelo**: Servidores podem solicitar conclusões sem incluir SDKs do LLM ou gerir o acesso ao modelo  
- **IA Iniciada pelo Servidor**: Permite que servidores gerem conteúdo autonomamente usando o modelo IA do cliente  
- **Interações Recursivas com LLM**: Suporta cenários complexos onde servidores precisam de assistência IA para processamento  
- **Geração Dinâmica de Conteúdo**: Permite que servidores criem respostas contextuais usando o modelo do host  
- **Suporte a Chamada de Ferramentas**: Servidores podem incluir os parâmetros `tools` e `toolChoice` para permitir que o modelo do cliente invoque ferramentas durante a amostragem

A amostragem é iniciada através do método `sampling/complete`, onde os servidores enviam pedidos de conclusão aos clientes.

### Raízes

As **Raízes** fornecem uma forma padronizada para clientes exporem limites do sistema de ficheiros aos servidores, ajudando os servidores a compreender que diretórios e ficheiros têm acesso:

- **Limites do Sistema de Ficheiros**: Definem os limites de onde os servidores podem operar dentro do sistema de ficheiros  
- **Controlo de Acesso**: Ajudam os servidores a perceber quais os diretórios e ficheiros a que têm permissão para aceder  
- **Atualizações Dinâmicas**: Clientes podem notificar servidores quando a lista de raízes muda  
- **Identificação Baseada em URI**: Raízes usam URIs `file://` para identificar diretórios e ficheiros acessíveis

As raízes são descobertas por meio do método `roots/list`, com os clientes a enviar notificações `notifications/roots/list_changed` quando as raízes mudam.

### Solicitação de Informação (Elicitação)

A **Solicitação de Informação** permite que servidores peçam informações adicionais ou confirmações aos utilizadores através da interface do cliente:

- **Pedidos de Entrada do Utilizador**: Servidores podem pedir informação adicional quando necessária para execução de ferramentas  
- **Diálogos de Confirmação**: Solicitar aprovação do utilizador para operações sensíveis ou impactantes  
- **Fluxos de Trabalho Interativos**: Permitem que servidores criem interações passo a passo com o utilizador  
- **Recolha Dinâmica de Parâmetros**: Recolhem parâmetros em falta ou opcionais durante a execução de ferramentas

Pedidos de solicitação são feitos usando o método `elicitation/request` para recolher a entrada do utilizador pela interface do cliente.

**Modalidade URL para Solicitação**: Servidores também podem pedir interações baseadas em URL, permitindo direcionar os utilizadores a páginas web externas para autenticação, confirmação ou inserção de dados.

### Registo

O **Registo** permite que servidores enviem mensagens de log estruturadas para clientes para debug, monitorização e visibilidade operacional:

- **Suporte a Debug**: Permite que servidores forneçam registos detalhados de execução para resolução de problemas  
- **Monitorização Operacional**: Enviar atualizações de estado e métricas de desempenho aos clientes  
- **Relato de Erros**: Fornece contexto detalhado de erro e informação diagnóstico  
- **Rastros de Auditoria**: Criar registos abrangentes das operações e decisões do servidor

Mensagens de registo são enviadas aos clientes para fornecer transparência nas operações do servidor e facilitar a depuração.

## Fluxo de Informação no MCP

O Model Context Protocol (MCP) define um fluxo estruturado de informação entre hosts, clientes, servidores e modelos. Compreender este fluxo ajuda a clarificar como os pedidos do utilizador são processados e como ferramentas externas e dados são integrados nas respostas do modelo.
- **O Host Inicia a Ligação**  
  A aplicação host (como um IDE ou interface de chat) estabelece uma ligação a um servidor MCP, tipicamente via STDIO, WebSocket ou outro transporte suportado.

- **Negociação de Capacidades**  
  O cliente (incorporado no host) e o servidor trocam informação sobre as suas funcionalidades, ferramentas, recursos e versões de protocolo suportadas. Isto garante que ambos os lados compreendem as capacidades disponíveis para a sessão.

- **Pedido do Utilizador**  
  O utilizador interage com o host (ex.: insere um prompt ou comando). O host recolhe esta entrada e passa-a ao cliente para processamento.

- **Utilização de Recurso ou Ferramenta**  
  - O cliente pode solicitar contexto adicional ou recursos ao servidor (como ficheiros, entradas em bases de dados ou artigos em bases de conhecimento) para enriquecer a compreensão do modelo.  
  - Se o modelo determinar que uma ferramenta é necessária (ex.: para obter dados, executar um cálculo ou chamar uma API), o cliente envia um pedido de invocação da ferramenta ao servidor, especificando o nome da ferramenta e os parâmetros.

- **Execução no Servidor**  
  O servidor recebe o pedido de recurso ou ferramenta, executa as operações necessárias (como executar uma função, consultar uma base de dados ou recuperar um ficheiro) e devolve os resultados ao cliente num formato estruturado.

- **Geração de Resposta**  
  O cliente integra as respostas do servidor (dados do recurso, resultados das ferramentas, etc.) na interação contínua com o modelo. O modelo usa esta informação para gerar uma resposta abrangente e relevante no contexto.

- **Apresentação do Resultado**  
  O host recebe a saída final do cliente e apresenta-a ao utilizador, frequentemente incluindo tanto o texto gerado pelo modelo como quaisquer resultados das execuções das ferramentas ou buscas de recursos.

Este fluxo permite ao MCP suportar aplicações de IA avançadas, interativas e conscientes do contexto, ligando modelos a ferramentas externas e fontes de dados de forma fluída.

## Arquitectura e Camadas do Protocolo

O MCP consiste em duas camadas arquitectónicas distintas que trabalham em conjunto para fornecer uma estrutura completa de comunicação:

### Camada de Dados

A **Camada de Dados** implementa o núcleo do protocolo MCP usando **JSON-RPC 2.0** como base. Esta camada define a estrutura das mensagens, semântica e padrões de interação:

#### Componentes Principais:

- **Protocolo JSON-RPC 2.0**: Toda a comunicação utiliza o formato de mensagem JSON-RPC 2.0 padronizado para chamadas de método, respostas e notificações  
- **Gestão do Ciclo de Vida**: Lida com a inicialização da ligação, negociação de capacidades e terminação da sessão entre clientes e servidores  
- **Primitivas de Servidor**: Permite aos servidores fornecer funcionalidades centrais através de ferramentas, recursos e prompts  
- **Primitivas de Cliente**: Permite aos servidores solicitar amostragem de LLMs, recolher input do utilizador e enviar mensagens de registo  
- **Notificações em Tempo Real**: Suporta notificações assíncronas para atualizações dinâmicas sem necessidade de polling

#### Funcionalidades Chave:

- **Negociação de Versão do Protocolo**: Usa versionamento baseado em datas (AAAA-MM-DD) para garantir compatibilidade  
- **Descoberta de Capacidades**: Clientes e servidores trocam informação sobre funcionalidades suportadas durante a inicialização  
- **Sessões Stateful**: Mantém estado da ligação ao longo de múltiplas interações para continuidade do contexto

### Camada de Transporte

A **Camada de Transporte** gere os canais de comunicação, formatação das mensagens e autenticação entre os participantes MCP:

#### Mecanismos de Transporte Suportados:

1. **Transporte STDIO**:  
   - Usa fluxos standard de entrada/saída para comunicação direta entre processos  
   - Óptimo para processos locais na mesma máquina sem overhead de rede  
   - Usado frequentemente em implementações locais de servidores MCP

2. **Transporte HTTP Streamable**:  
   - Usa HTTP POST para mensagens do cliente para o servidor  
   - Opcionalmente suporta Server-Sent Events (SSE) para streaming do servidor para o cliente  
   - Permite comunicação remota entre servidores através de redes  
   - Suporta autenticação HTTP padrão (tokens bearer, chaves API, cabeçalhos personalizados)  
   - O MCP recomenda OAuth para autenticação segura baseada em tokens

#### Abstração do Transporte:

A camada de transporte abstrai detalhes de comunicação da camada de dados, permitindo que o mesmo formato de mensagem JSON-RPC 2.0 opere em todos os mecanismos de transporte. Esta abstração permite que aplicações alternem entre servidores locais e remotos sem esforço.

### Considerações de Segurança

As implementações MCP devem cumprir vários princípios críticos de segurança para garantir interações seguras, confiáveis e protegidas em todas as operações do protocolo:

- **Consentimento e Controlo do Utilizador**: Os utilizadores devem fornecer consentimento explícito antes de qualquer dado ser acedido ou operação executada. Devem ter controlo claro sobre os dados partilhados e as ações autorizadas, suportados por interfaces intuitivas para rever e aprovar atividades.

- **Privacidade dos Dados**: Dados dos utilizadores só devem ser expostos com consentimento explícito e protegidos por controlos de acesso adequados. As implementações MCP devem proteger contra a transmissão não autorizada de dados e garantir manutenção da privacidade em todas as interações.

- **Segurança das Ferramentas**: Antes de invocar qualquer ferramenta, é necessário consentimento explícito do utilizador. Os utilizadores devem compreender claramente a funcionalidade de cada ferramenta, e limites rigorosos de segurança devem ser aplicados para prevenir execuções não intencionais ou inseguras.

Ao seguir estes princípios de segurança, o MCP assegura a confiança, privacidade e segurança dos utilizadores em todas as interações do protocolo, ao mesmo tempo que possibilita integrações poderosas de IA.

## Exemplos de Código: Componentes Chave

A seguir estão exemplos de código em várias linguagens populares que ilustram como implementar componentes-chave de servidores MCP e ferramentas.

### Exemplo .NET: Criar um Servidor MCP Simples com Ferramentas

Aqui está um exemplo prático de código .NET a demonstrar como implementar um servidor MCP simples com ferramentas personalizadas. Este exemplo mostra como definir e registar ferramentas, tratar pedidos e ligar o servidor usando o Model Context Protocol.

```csharp
using System;
using System.Threading.Tasks;
using ModelContextProtocol.Server;
using ModelContextProtocol.Server.Transport;
using ModelContextProtocol.Server.Tools;

public class WeatherServer
{
    public static async Task Main(string[] args)
    {
        // Create an MCP server
        var server = new McpServer(
            name: "Weather MCP Server",
            version: "1.0.0"
        );
        
        // Register our custom weather tool
        server.AddTool<string, WeatherData>("weatherTool", 
            description: "Gets current weather for a location",
            execute: async (location) => {
                // Call weather API (simplified)
                var weatherData = await GetWeatherDataAsync(location);
                return weatherData;
            });
        
        // Connect the server using stdio transport
        var transport = new StdioServerTransport();
        await server.ConnectAsync(transport);
        
        Console.WriteLine("Weather MCP Server started");
        
        // Keep the server running until process is terminated
        await Task.Delay(-1);
    }
    
    private static async Task<WeatherData> GetWeatherDataAsync(string location)
    {
        // This would normally call a weather API
        // Simplified for demonstration
        await Task.Delay(100); // Simulate API call
        return new WeatherData { 
            Temperature = 72.5,
            Conditions = "Sunny",
            Location = location
        };
    }
}

public class WeatherData
{
    public double Temperature { get; set; }
    public string Conditions { get; set; }
    public string Location { get; set; }
}
```

### Exemplo Java: Componentes de Servidor MCP

Este exemplo demonstra o mesmo servidor MCP e registo de ferramentas do exemplo .NET acima, mas implementado em Java.

```java
import io.modelcontextprotocol.server.McpServer;
import io.modelcontextprotocol.server.McpToolDefinition;
import io.modelcontextprotocol.server.transport.StdioServerTransport;
import io.modelcontextprotocol.server.tool.ToolExecutionContext;
import io.modelcontextprotocol.server.tool.ToolResponse;

public class WeatherMcpServer {
    public static void main(String[] args) throws Exception {
        // Criar um servidor MCP
        McpServer server = McpServer.builder()
            .name("Weather MCP Server")
            .version("1.0.0")
            .build();
            
        // Registar uma ferramenta de meteorologia
        server.registerTool(McpToolDefinition.builder("weatherTool")
            .description("Gets current weather for a location")
            .parameter("location", String.class)
            .execute((ToolExecutionContext ctx) -> {
                String location = ctx.getParameter("location", String.class);
                
                // Obter dados meteorológicos (simplificado)
                WeatherData data = getWeatherData(location);
                
                // Retornar resposta formatada
                return ToolResponse.content(
                    String.format("Temperature: %.1f°F, Conditions: %s, Location: %s", 
                    data.getTemperature(), 
                    data.getConditions(), 
                    data.getLocation())
                );
            })
            .build());
        
        // Ligar o servidor usando transporte stdio
        try (StdioServerTransport transport = new StdioServerTransport()) {
            server.connect(transport);
            System.out.println("Weather MCP Server started");
            // Manter o servidor em execução até o processo ser terminado
            Thread.currentThread().join();
        }
    }
    
    private static WeatherData getWeatherData(String location) {
        // A implementação chamaria uma API de meteorologia
        // Simplificado para fins de exemplo
        return new WeatherData(72.5, "Sunny", location);
    }
}

class WeatherData {
    private double temperature;
    private String conditions;
    private String location;
    
    public WeatherData(double temperature, String conditions, String location) {
        this.temperature = temperature;
        this.conditions = conditions;
        this.location = location;
    }
    
    public double getTemperature() {
        return temperature;
    }
    
    public String getConditions() {
        return conditions;
    }
    
    public String getLocation() {
        return location;
    }
}
```

### Exemplo Python: Construir um Servidor MCP

Este exemplo usa fastmcp, por favor certifique-se de o instalar primeiro:

```python
pip install fastmcp
```
Exemplo de Código:

```python
#!/usr/bin/env python3
import asyncio
from fastmcp import FastMCP
from fastmcp.transports.stdio import serve_stdio

# Criar um servidor FastMCP
mcp = FastMCP(
    name="Weather MCP Server",
    version="1.0.0"
)

@mcp.tool()
def get_weather(location: str) -> dict:
    """Gets current weather for a location."""
    return {
        "temperature": 72.5,
        "conditions": "Sunny",
        "location": location
    }

# Abordagem alternativa usando uma classe
class WeatherTools:
    @mcp.tool()
    def forecast(self, location: str, days: int = 1) -> dict:
        """Gets weather forecast for a location for the specified number of days."""
        return {
            "location": location,
            "forecast": [
                {"day": i+1, "temperature": 70 + i, "conditions": "Partly Cloudy"}
                for i in range(days)
            ]
        }

# Registar ferramentas da classe
weather_tools = WeatherTools()

# Iniciar o servidor
if __name__ == "__main__":
    asyncio.run(serve_stdio(mcp))
```

### Exemplo JavaScript: Criar um Servidor MCP

Este exemplo mostra a criação de servidor MCP em JavaScript e como registar duas ferramentas relacionadas com o tempo.

```javascript
// Utilizando o SDK oficial do Protocolo de Contexto do Modelo
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod"; // Para validação de parâmetros

// Criar um servidor MCP
const server = new McpServer({
  name: "Weather MCP Server",
  version: "1.0.0"
});

// Definir uma ferramenta de meteorologia
server.tool(
  "weatherTool",
  {
    location: z.string().describe("The location to get weather for")
  },
  async ({ location }) => {
    // Normalmente isto chamaria uma API de meteorologia
    // Simplificado para demonstração
    const weatherData = await getWeatherData(location);
    
    return {
      content: [
        { 
          type: "text", 
          text: `Temperature: ${weatherData.temperature}°F, Conditions: ${weatherData.conditions}, Location: ${weatherData.location}` 
        }
      ]
    };
  }
);

// Definir uma ferramenta de previsão
server.tool(
  "forecastTool",
  {
    location: z.string(),
    days: z.number().default(3).describe("Number of days for forecast")
  },
  async ({ location, days }) => {
    // Normalmente isto chamaria uma API de meteorologia
    // Simplificado para demonstração
    const forecast = await getForecastData(location, days);
    
    return {
      content: [
        { 
          type: "text", 
          text: `${days}-day forecast for ${location}: ${JSON.stringify(forecast)}` 
        }
      ]
    };
  }
);

// Funções auxiliares
async function getWeatherData(location) {
  // Simular chamada de API
  return {
    temperature: 72.5,
    conditions: "Sunny",
    location: location
  };
}

async function getForecastData(location, days) {
  // Simular chamada de API
  return Array.from({ length: days }, (_, i) => ({
    day: i + 1,
    temperature: 70 + Math.floor(Math.random() * 10),
    conditions: i % 2 === 0 ? "Sunny" : "Partly Cloudy"
  }));
}

// Conectar o servidor usando transporte stdio
const transport = new StdioServerTransport();
server.connect(transport).catch(console.error);

console.log("Weather MCP Server started");
```

Este exemplo JavaScript demonstra como criar um servidor MCP que regista ferramentas relacionadas com o tempo e liga usando transporte stdio para lidar com pedidos de clientes.

## Segurança e Autorização

O MCP inclui vários conceitos e mecanismos integrados para gerir segurança e autorização ao longo do protocolo:

1. **Controlo de Permissões de Ferramentas**:  
  Os clientes podem especificar quais ferramentas um modelo pode usar durante uma sessão. Isto garante que apenas ferramentas explicitamente autorizadas estão acessíveis, reduzindo o risco de operações não intencionais ou inseguras. Permissões podem ser configuradas dinamicamente com base em preferências do utilizador, políticas organizacionais ou contexto da interação.

2. **Autenticação**:  
  Os servidores podem exigir autenticação antes de conceder acesso a ferramentas, recursos ou operações sensíveis. Isto pode envolver chaves API, tokens OAuth ou outros esquemas de autenticação. A autenticação adequada assegura que apenas clientes e utilizadores confiáveis possam invocar capacidades do lado do servidor.

3. **Validação**:  
  A validação de parâmetros é aplicada para todas as invocações de ferramentas. Cada ferramenta define os tipos esperados, formatos e restrições para os seus parâmetros, e o servidor valida os pedidos recebidos em conformidade. Isto previne entradas mal formadas ou maliciosas de alcançarem implementações de ferramentas e ajuda a manter a integridade das operações.

4. **Limitação de Taxa**:  
  Para prevenir abusos e garantir uso justo dos recursos do servidor, os servidores MCP podem implementar limitação de taxa para chamadas a ferramentas e acesso a recursos. Os limites podem ser aplicados por utilizador, por sessão ou globalmente, ajudando a proteger contra ataques de negação de serviço ou consumo excessivo de recursos.

Combinando estes mecanismos, o MCP fornece uma base segura para integrar modelos de linguagem com ferramentas externas e fontes de dados, oferecendo aos utilizadores e programadores controlo refinado sobre o acesso e uso.

## Mensagens do Protocolo & Fluxo de Comunicação

A comunicação MCP usa mensagens estruturadas **JSON-RPC 2.0** para facilitar interações claras e fiáveis entre hosts, clientes e servidores. O protocolo define padrões específicos de mensagens para diferentes tipos de operações:

### Tipos de Mensagens Centrais:

#### **Mensagens de Inicialização**  
- Pedido `initialize`: Estabelece ligação e negocia versão do protocolo e capacidades  
- Resposta `initialize`: Confirma funcionalidades suportadas e informações do servidor  
- `notifications/initialized`: Indica que a inicialização está concluída e a sessão pronta

#### **Mensagens de Descoberta**  
- Pedido `tools/list`: Descobre ferramentas disponíveis no servidor  
- Pedido `resources/list`: Lista recursos (fontes de dados) disponíveis  
- Pedido `prompts/list`: Obtém templates de prompts disponíveis

#### **Mensagens de Execução**  
- Pedido `tools/call`: Executa uma ferramenta específica com parâmetros fornecidos  
- Pedido `resources/read`: Recupera conteúdo de um recurso específico  
- Pedido `prompts/get`: Buscador um template de prompt com parâmetros opcionais

#### **Mensagens do Lado do Cliente**  
- Pedido `sampling/complete`: Servidor solicita conclusão LLM ao cliente  
- Pedido `elicitation/request`: Servidor solicita input do utilizador via interface do cliente  
- Mensagens de registo: Servidor envia mensagens de log estruturadas ao cliente

#### **Mensagens de Notificação**  
- `notifications/tools/list_changed`: Servidor notifica cliente sobre alterações nas ferramentas  
- `notifications/resources/list_changed`: Servidor notifica cliente sobre alterações nos recursos  
- `notifications/prompts/list_changed`: Servidor notifica cliente sobre alterações nos prompts

### Estrutura da Mensagem:

Todas as mensagens MCP seguem o formato JSON-RPC 2.0 com:  
- Mensagens de Pedido: incluem `id`, `method` e `params` opcionais  
- Mensagens de Resposta: incluem `id` e ou `result` ou `error`  
- Mensagens de Notificação: incluem `method` e `params` opcionais (sem `id` nem resposta esperada)

Esta comunicação estruturada garante interações fiáveis, rastreáveis e extensíveis, suportando cenários avançados como atualizações em tempo real, encadeamento de ferramentas e tratamento robusto de erros.

### Tarefas (Experimental)

**Tarefas** são uma funcionalidade experimental que fornece invólucros de execução duráveis permitindo obtenção de resultados diferidos e rastreio de estado para pedidos MCP:

- **Operações de Longa Duração**: Rastreia cálculos dispendiosos, automação de fluxos de trabalho e processamento em lote  
- **Resultados Diferidos**: Permite polling do estado da tarefa e obtenção dos resultados quando as operações terminam  
- **Rastreamento de Estado**: Monitora progresso da tarefa através de estados definidos no ciclo de vida  
- **Operações Multi-passo**: Suporta workflows complexos que abrangem múltiplas interações

As tarefas envolvem pedidos MCP padrão para permitir padrões de execução assíncrona para operações que não podem ser concluídas imediatamente.

## Conclusões Principais

- **Arquitectura**: MCP usa uma arquitectura cliente-servidor onde hosts gerem múltiplas ligações de clientes a servidores  
- **Participantes**: O ecossistema inclui hosts (aplicações IA), clientes (conectores de protocolo) e servidores (fornecedores de capacidades)  
- **Mecanismos de Transporte**: Comunicação suporta STDIO (local) e HTTP Streamable com SSE opcional (remoto)  
- **Primitivas Centrais**: Servidores expõem ferramentas (funções executáveis), recursos (fontes de dados) e prompts (templates)  
- **Primitivas de Cliente**: Servidores podem solicitar amostragem (LLM com suporte a chamadas a ferramentas), elicitação (input do utilizador incluindo modo URL), limites de sistema de ficheiros (roots) e registo a partir dos clientes  
- **Funcionalidades Experimentais**: Tarefas fornecem invólucros de execução duráveis para operações de longa duração  
- **Fundamento do Protocolo**: Construído sobre JSON-RPC 2.0 com versionamento baseado em datas (atual: 2025-11-25)  
- **Capacidades em Tempo Real**: Suporta notificações para atualizações dinâmicas e sincronização em tempo real  
- **Segurança em Primeiro Lugar**: Consentimento explícito do utilizador, proteção da privacidade dos dados e transporte seguro são requisitos centrais

## Exercício

Desenhe uma ferramenta MCP simples que seria útil no seu domínio. Defina:  
1. Qual seria o nome da ferramenta  
2. Quais parâmetros aceitaria  
3. Que saída devolveria  
4. Como um modelo poderia usar esta ferramenta para resolver problemas do utilizador


---

## O que vem a seguir

Próximo: [Capítulo 2: Segurança](../02-Security/README.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Aviso Legal**:
Este documento foi traduzido utilizando o serviço de tradução automática [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos por garantir a precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte oficial. Para informações críticas, recomenda-se a tradução profissional por um ser humano. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações erradas resultantes da utilização desta tradução.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->