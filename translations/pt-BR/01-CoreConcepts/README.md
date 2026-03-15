# Conceitos Básicos do MCP: Dominando o Protocolo de Contexto do Modelo para Integração de IA

[![Conceitos Básicos do MCP](../../../translated_images/pt-BR/02.8203e26c6fb5a797.webp)](https://youtu.be/earDzWGtE84)

_(Clique na imagem acima para assistir ao vídeo desta lição)_

O [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) é uma estrutura poderosa e padronizada que otimiza a comunicação entre Grandes Modelos de Linguagem (LLMs) e ferramentas externas, aplicações e fontes de dados.  
Este guia lhe conduzirá pelos conceitos básicos do MCP. Você aprenderá sobre sua arquitetura cliente-servidor, componentes essenciais, mecânicas de comunicação e melhores práticas de implementação.

- **Consentimento Explícito do Usuário**: Todo acesso e operação de dados requer aprovação explícita do usuário antes da execução. Os usuários devem compreender claramente quais dados serão acessados e quais ações serão realizadas, com controle granular sobre permissões e autorizações.

- **Proteção da Privacidade dos Dados**: Dados do usuário são expostos apenas com consentimento explícito e devem ser protegidos por controles robustos durante todo o ciclo de interação. Implementações devem prevenir transmissão não autorizada e manter limites rigorosos de privacidade.

- **Segurança na Execução de Ferramentas**: Toda invocação de ferramenta requer consentimento explícito do usuário com compreensão clara da funcionalidade, parâmetros e impacto potencial da ferramenta. Limites de segurança robustos previnem execuções inseguras, não intencionais ou maliciosas.

- **Segurança da Camada de Transporte**: Todos os canais de comunicação devem usar mecanismos adequados de criptografia e autenticação. Conexões remotas devem implementar protocolos seguros de transporte e gestão adequada de credenciais.

#### Diretrizes de Implementação:

- **Gerenciamento de Permissões**: Implemente sistemas de permissões detalhados que permitam ao usuário controlar quais servidores, ferramentas e recursos são acessíveis  
- **Autenticação & Autorização**: Use métodos seguros de autenticação (OAuth, chaves de API) com gestão adequada de tokens e expiração  
- **Validação de Entrada**: Valide todos os parâmetros e entradas de dados conforme esquemas definidos para prevenir ataques por injeção  
- **Log de Auditoria**: Mantenha registros abrangentes de todas as operações para monitoramento de segurança e conformidade

## Visão Geral

Esta lição explora a arquitetura fundamental e os componentes que compõem o ecossistema do Model Context Protocol (MCP). Você aprenderá sobre a arquitetura cliente-servidor, componentes-chave e mecanismos de comunicação que alimentam as interações do MCP.

## Objetivos Principais de Aprendizagem

Ao final desta lição, você será capaz de:

- Compreender a arquitetura cliente-servidor do MCP.  
- Identificar papéis e responsabilidades de Hosts, Clients e Servers.  
- Analisar as características centrais que tornam o MCP uma camada de integração flexível.  
- Aprender como a informação flui dentro do ecossistema MCP.  
- Obter insights práticos por meio de exemplos de código em .NET, Java, Python e JavaScript.

## Arquitetura do MCP: Um Olhar Mais Profundo

O ecossistema MCP é construído sobre um modelo cliente-servidor. Esta estrutura modular permite que aplicações de IA interajam eficientemente com ferramentas, bancos de dados, APIs e recursos contextuais. Vamos detalhar essa arquitetura em seus componentes principais.

Na essência, o MCP segue a arquitetura cliente-servidor onde uma aplicação host pode se conectar a múltiplos servidores:

```mermaid
flowchart LR
    subgraph "Seu Computador"
        Host["Hospedeiro com MCP (Visual Studio, VS Code, IDEs, Ferramentas)"]
        S1["Servidor MCP A"]
        S2["Servidor MCP B"]
        S3["Servidor MCP C"]
        Host <-->|"Protocolo MCP"| S1
        Host <-->|"Protocolo MCP"| S2
        Host <-->|"Protocolo MCP"| S3
        S1 <--> D1[("Local\Fonte de Dados A")]
        S2 <--> D2[("Local\Fonte de Dados B")]
    end
    subgraph "Internet"
        S3 <-->|"APIs Web"| D3[("Serviços Remotos")]
    end
```
- **Hosts do MCP**: Programas como VSCode, Claude Desktop, IDEs ou ferramentas de IA que desejam acessar dados via MCP  
- **Clientes MCP**: Clientes de protocolo que mantêm conexões 1:1 com servidores  
- **Servidores MCP**: Programas leves que expõem capacidades específicas através do protocolo padronizado Model Context Protocol  
- **Fontes de Dados Locais**: Arquivos, bancos de dados e serviços do seu computador que os servidores MCP podem acessar com segurança  
- **Serviços Remotos**: Sistemas externos disponíveis pela internet que servidores MCP podem acessar via APIs.

O Protocolo MCP é um padrão em evolução que usa versionamento baseado em datas (formato AAAA-MM-DD). A versão atual do protocolo é **2025-11-25**. Você pode conferir as atualizações mais recentes na [especificação do protocolo](https://modelcontextprotocol.io/specification/2025-11-25/)

### 1. Hosts

No Model Context Protocol (MCP), **Hosts** são aplicações de IA que atuam como interface principal pela qual usuários interagem com o protocolo. Hosts coordenam e gerenciam conexões com múltiplos servidores MCP criando clientes MCP dedicados para cada conexão de servidor. Exemplos de Hosts incluem:

- **Aplicações de IA**: Claude Desktop, Visual Studio Code, Claude Code  
- **Ambientes de Desenvolvimento**: IDEs e editores de código com integração MCP  
- **Aplicações Personalizadas**: Agentes e ferramentas de IA construídos para propósitos específicos

**Hosts** são aplicações que coordenam interações com modelos de IA. Eles:

- **Orquestram Modelos de IA**: Executam ou interagem com LLMs para gerar respostas e coordenar fluxos de trabalho de IA  
- **Gerenciam Conexões dos Clientes**: Criam e mantêm um cliente MCP por conexão a servidor MCP  
- **Controlam Interface do Usuário**: Lidam com fluxo da conversa, interações do usuário e apresentação de respostas  
- **Impoem Segurança**: Controlam permissões, restrições de segurança e autenticação  
- **Gerenciam Consentimento do Usuário**: Administram aprovação do usuário para compartilhamento de dados e execução de ferramentas  

### 2. Clientes

**Clientes** são componentes essenciais que mantêm conexões dedicadas um-para-um entre Hosts e servidores MCP. Cada cliente MCP é instanciado pelo Host para conectar-se a um servidor MCP específico, garantindo canais de comunicação organizados e seguros. Múltiplos clientes permitem que Hosts conectem-se a múltiplos servidores simultaneamente.

**Clientes** são componentes conectores dentro da aplicação host. Eles:

- **Comunicação de Protocolo**: Enviam requisições JSON-RPC 2.0 aos servidores com prompts e instruções  
- **Negociação de Capacidades**: Negociam funcionalidades suportadas e versões de protocolo com servidores durante inicialização  
- **Execução de Ferramentas**: Gerenciam pedidos de execução de ferramentas a partir de modelos e processam respostas  
- **Atualizações em Tempo Real**: Lidam com notificações e atualizações em tempo real dos servidores  
- **Processamento de Respostas**: Processam e formatam respostas do servidor para exibição ao usuário

### 3. Servidores

**Servidores** são programas que fornecem contexto, ferramentas e capacidades aos clientes MCP. Podem ser executados localmente (na mesma máquina que o Host) ou remotamente (em plataformas externas) e são responsáveis por tratar requisições dos clientes e fornecer respostas estruturadas. Servidores expõem funcionalidades específicas através do protocolo padronizado Model Context Protocol.

**Servidores** são serviços que fornecem contexto e capacidades. Eles:

- **Registro de Funcionalidades**: Registram e expõem primitivas disponíveis (recursos, prompts, ferramentas) para clientes  
- **Processamento de Requisições**: Recebem e executam chamadas de ferramentas, pedidos de recursos e prompts dos clientes  
- **Fornecimento de Contexto**: Oferecem informações contextuais e dados para enriquecer as respostas dos modelos  
- **Gerenciamento de Estado**: Mantêm estado de sessão e lidam com interações com estado quando necessário  
- **Notificações em Tempo Real**: Enviam notificações sobre mudanças de capacidades e atualizações para clientes conectados

Servidores podem ser desenvolvidos por qualquer pessoa para estender as capacidades do modelo com funcionalidades especializadas, e suportam cenários de implantação locais e remotos.

### 4. Primitivas do Servidor

Servidores no Model Context Protocol (MCP) oferecem três **primitivas** centrais que definem os blocos fundamentais para interações ricas entre clientes, hosts e modelos de linguagem. Essas primitivas especificam os tipos de informação contextual e ações disponíveis pelo protocolo.

Servidores MCP podem expor qualquer combinação das três primitivas centrais abaixo:

#### Recursos

**Recursos** são fontes de dados que fornecem informações contextuais para aplicações de IA. Eles representam conteúdo estático ou dinâmico que pode melhorar o entendimento e a tomada de decisão do modelo:

- **Dados Contextuais**: Informações estruturadas e contexto para consumo do modelo de IA  
- **Bases de Conhecimento**: Repositórios de documentos, artigos, manuais e trabalhos de pesquisa  
- **Fontes de Dados Locais**: Arquivos, bancos de dados e informações do sistema local  
- **Dados Externos**: Respostas de APIs, serviços web e dados de sistemas remotos  
- **Conteúdo Dinâmico**: Dados em tempo real que se atualizam com base em condições externas

Recursos são identificados por URIs e suportam descoberta através dos métodos `resources/list` e recuperação via `resources/read`:

```text
file://documents/project-spec.md
database://production/users/schema
api://weather/current
```

#### Prompts

**Prompts** são templates reutilizáveis que ajudam a estruturar interações com modelos de linguagem. Fornecem padrões padronizados de interação e fluxos de trabalho modelados:

- **Interações Baseadas em Template**: Mensagens pré-estruturadas e iniciadores de conversação  
- **Modelos de Fluxo de Trabalho**: Sequências padronizadas para tarefas e interações comuns  
- **Exemplos Few-shot**: Templates baseados em exemplos para instrução do modelo  
- **Prompts de Sistema**: Prompts fundamentais que definem o comportamento e o contexto do modelo  
- **Templates Dinâmicos**: Prompts parametrizados que se adaptam a contextos específicos

Prompts suportam substituição de variáveis e podem ser descobertos via `prompts/list` e recuperados com `prompts/get`:

```markdown
Generate a {{task_type}} for {{product}} targeting {{audience}} with the following requirements: {{requirements}}
```

#### Ferramentas

**Ferramentas** são funções executáveis que modelos de IA podem invocar para realizar ações específicas. Representam os "verbos" do ecossistema MCP, permitindo a modelos interagir com sistemas externos:

- **Funções Executáveis**: Operações discretas que modelos podem invocar com parâmetros específicos  
- **Integração com Sistemas Externos**: Chamadas de API, consultas a banco de dados, operações em arquivos, cálculos  
- **Identidade Única**: Cada ferramenta tem nome distinto, descrição e esquema de parâmetros  
- **Entrada/Saída Estruturada**: Ferramentas aceitam parâmetros validados e retornam respostas estruturadas e tipadas  
- **Capacidades de Ação**: Permitem que modelos realizem ações no mundo real e recuperem dados ao vivo

Ferramentas são definidas com JSON Schema para validação de parâmetros e descobertas via `tools/list` e executadas por `tools/call`. Ferramentas também podem incluir **ícones** como metadados adicionais para melhor apresentação na interface.

**Anotações de Ferramenta**: Ferramentas suportam anotações comportamentais (por exemplo, `readOnlyHint`, `destructiveHint`) que descrevem se uma ferramenta é somente leitura ou destrutiva, auxiliando clientes a tomar decisões informadas sobre a execução.

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
    // Executa a busca e retorna resultados estruturados
    return await productService.search(params);
  }
);
```

## Primitivas Clientes

No Model Context Protocol (MCP), **clientes** podem expor primitivas que permitem que servidores solicitem capacidades adicionais da aplicação host. Essas primitivas do lado cliente possibilitam implementações de servidor mais ricas e interativas com acesso às capacidades do modelo de IA e interações com o usuário.

### Amostragem

**Amostragem** permite que servidores requisitem completações de modelo de linguagem a partir da aplicação de IA do cliente. Essa primitiva permite acesso às capacidades de LLM sem embutir dependências próprias do modelo:

- **Acesso Independente do Modelo**: Servidores podem requisitar completações sem incluir SDKs ou gerenciar acesso ao modelo LLM  
- **IA Iniciada pelo Servidor**: Habilita servidores a gerar conteúdo autonomamente usando modelo IA do cliente  
- **Interações Recursivas com LLM**: Suporta cenários complexos onde servidores precisam de apoio da IA para processamento  
- **Geração Dinâmica de Conteúdo**: Permite servidores criar respostas contextuais usando modelo do host  
- **Suporte a Chamadas de Ferramentas**: Servidores podem incluir parâmetros `tools` e `toolChoice` para habilitar o modelo do cliente a invocar ferramentas durante amostragem

A amostragem é iniciada através do método `sampling/complete`, onde servidores enviam pedidos de completamento aos clientes.

### Raízes

**Raízes** fornecem uma maneira padronizada para que clientes exponham limites do sistema de arquivos aos servidores, ajudando-os a compreender quais diretórios e arquivos têm acesso:

- **Limites do Sistema de Arquivos**: Definem onde servidores podem operar dentro do sistema de arquivos  
- **Controle de Acesso**: Auxiliam servidores a entender permissões de acesso a diretórios e arquivos  
- **Atualizações Dinâmicas**: Clientes podem notificar servidores quando a lista de raízes muda  
- **Identificação por URI**: Raízes usam URIs `file://` para identificar diretórios e arquivos acessíveis

Raízes são descobertas através do método `roots/list`, com clientes enviando notificações `notifications/roots/list_changed` quando mudam.

### Elicitação

**Elicitação** permite que servidores solicitem informações adicionais ou confirmação dos usuários através da interface do cliente:

- **Pedidos de Entrada do Usuário**: Servidores podem pedir informações extras necessárias para execução de ferramentas  
- **Caixas de Diálogo de Confirmação**: Solicitar aprovação do usuário para operações sensíveis ou de impacto  
- **Fluxos Interativos**: Permitem servidores criarem interações passo a passo com o usuário  
- **Coleta Dinâmica de Parâmetros**: Reunir parâmetros faltantes ou opcionais durante execução de ferramentas

Pedidos de elicitação são feitos mediante o método `elicitation/request` para coletar entrada do usuário via interface do cliente.

**Modo URL de Elicitação**: Servidores também podem solicitar interações via URL, permitindo que usuários sejam direcionados a páginas web externas para autenticação, confirmação ou entrada de dados.

### Registro de Logs

**Registro de Logs** permite que servidores enviem mensagens estruturadas de log para clientes para fins de depuração, monitoramento e visibilidade operacional:

- **Suporte à Depuração**: Permite que servidores forneçam logs detalhados para solução de problemas  
- **Monitoramento Operacional**: Envia atualizações de status e métricas de desempenho para clientes  
- **Relato de Erros**: Fornece contexto detalhado de erro e informações diagnósticas  
- **Traços de Auditoria**: Cria registros abrangentes das operações e decisões do servidor

Mensagens de log são enviadas para clientes para prover transparência nas operações do servidor e facilitar depuração.

## Fluxo de Informação no MCP

O Model Context Protocol (MCP) define um fluxo estruturado de informação entre hosts, clientes, servidores e modelos. Compreender esse fluxo ajuda a clarificar como os pedidos dos usuários são processados e como ferramentas externas e dados são integrados nas respostas dos modelos.
- **Host Inicia a Conexão**  
  A aplicação host (como uma IDE ou interface de chat) estabelece uma conexão com um servidor MCP, tipicamente via STDIO, WebSocket ou outro transporte suportado.

- **Negociação de Capacidades**  
  O cliente (embutido no host) e o servidor trocam informações sobre as funcionalidades, ferramentas, recursos e versões do protocolo que suportam. Isso garante que ambos os lados entendam quais capacidades estão disponíveis para a sessão.

- **Solicitação do Usuário**  
  O usuário interage com o host (ex: insere um prompt ou comando). O host coleta essa entrada e a passa para o cliente para processamento.

- **Uso de Recurso ou Ferramenta**  
  - O cliente pode solicitar contexto ou recursos adicionais ao servidor (como arquivos, entradas de banco de dados ou artigos da base de conhecimento) para enriquecer o entendimento do modelo.
  - Se o modelo determinar que uma ferramenta é necessária (ex: para obter dados, fazer um cálculo ou chamar uma API), o cliente envia uma solicitação de invocação da ferramenta ao servidor, especificando o nome da ferramenta e os parâmetros.

- **Execução no Servidor**  
  O servidor recebe a solicitação de recurso ou ferramenta, executa as operações necessárias (como rodar uma função, consultar um banco de dados ou recuperar um arquivo) e retorna os resultados ao cliente em formato estruturado.

- **Geração de Resposta**  
  O cliente integra as respostas do servidor (dados de recursos, saídas de ferramentas, etc.) na interação contínua do modelo. O modelo usa essas informações para gerar uma resposta abrangente e contextualmente relevante.

- **Apresentação do Resultado**  
  O host recebe o resultado final do cliente e o apresenta ao usuário, frequentemente incluindo tanto o texto gerado pelo modelo quanto quaisquer resultados de execuções de ferramentas ou consultas a recursos.

Esse fluxo permite que o MCP suporte aplicações de IA avançadas, interativas e conscientes do contexto ao conectar modelos com ferramentas externas e fontes de dados de forma fluida.

## Arquitetura e Camadas do Protocolo

O MCP consiste em duas camadas arquiteturais distintas que trabalham juntas para fornecer um framework completo de comunicação:

### Camada de Dados

A **Camada de Dados** implementa o protocolo central do MCP usando **JSON-RPC 2.0** como base. Essa camada define a estrutura das mensagens, semântica e padrões de interação:

#### Componentes Principais:

- **Protocolo JSON-RPC 2.0**: Toda comunicação usa o formato padrão de mensagens JSON-RPC 2.0 para chamadas de método, respostas e notificações
- **Gerenciamento de Ciclo de Vida**: Trata da inicialização da conexão, negociação de capacidades e término da sessão entre clientes e servidores
- **Primitivas do Servidor**: Permite que servidores forneçam funcionalidade principal através de ferramentas, recursos e prompts
- **Primitivas do Cliente**: Permite que servidores solicitem amostragem de LLMs, obtenção de entrada do usuário e envio de mensagens de log
- **Notificações em Tempo Real**: Suporta notificações assíncronas para atualizações dinâmicas sem polling

#### Recursos Chave:

- **Negociação de Versão do Protocolo**: Usa versionamento baseado em data (YYYY-MM-DD) para garantir compatibilidade
- **Descoberta de Capacidades**: Clientes e servidores trocam informações sobre recursos suportados durante a inicialização
- **Sessões com Estado**: Mantém o estado da conexão por múltiplas interações para continuidade do contexto

### Camada de Transporte

A **Camada de Transporte** gerencia os canais de comunicação, o framing das mensagens e a autenticação entre participantes do MCP:

#### Mecanismos de Transporte Suportados:

1. **Transporte STDIO**:
   - Usa fluxos de entrada/saída padrão para comunicação direta entre processos
   - Ideal para processos locais na mesma máquina sem overhead de rede
   - Comumente usado para implementações locais de servidores MCP

2. **Transporte HTTP Streamable**:
   - Usa HTTP POST para mensagens cliente-servidor  
   - Suporta opcionalmente Server-Sent Events (SSE) para streaming do servidor para o cliente
   - Permite comunicação remota com servidores através de redes
   - Suporta autenticação HTTP padrão (tokens bearer, chaves API, headers customizados)
   - O MCP recomenda OAuth para autenticação segura baseada em tokens

#### Abstração do Transporte:

A camada de transporte abstrai os detalhes da comunicação da camada de dados, permitindo o mesmo formato de mensagem JSON-RPC 2.0 em todos os mecanismos de transporte. Essa abstração permite que aplicações alternem de servidores locais para remotos sem problemas.

### Considerações de Segurança

Implementações MCP devem seguir vários princípios críticos de segurança para garantir interações seguras, confiáveis e protegidas em todas as operações do protocolo:

- **Consentimento e Controle do Usuário**: Usuários devem fornecer consentimento explícito antes que quaisquer dados sejam acessados ou operações executadas. Eles devem possuir controle claro sobre quais dados são compartilhados e quais ações são autorizadas, apoiados por interfaces intuitivas para revisão e aprovação.

- **Privacidade dos Dados**: Dados do usuário devem ser expostos somente com consentimento explícito e protegidos por controles adequados de acesso. Implementações MCP devem prevenir transmissões não autorizadas e assegurar a privacidade ao longo de todas as interações.

- **Segurança das Ferramentas**: Antes de invocar qualquer ferramenta, é necessário consentimento explícito do usuário. Usuários devem compreender claramente a funcionalidade de cada ferramenta e limites robustos de segurança devem ser aplicados para evitar execuções indevidas ou inseguras.

Seguindo esses princípios de segurança, o MCP assegura a confiança, privacidade e segurança do usuário em todas as interações do protocolo enquanto permite integrações poderosas de IA.

## Exemplos de Código: Componentes Principais

A seguir, exemplos de código em algumas linguagens populares que ilustram como implementar componentes-chave do servidor MCP e suas ferramentas.

### Exemplo .NET: Criando um Servidor MCP Simples com Ferramentas

Aqui está um exemplo prático em .NET demonstrando como implementar um servidor MCP simples com ferramentas personalizadas. Este exemplo mostra como definir e registrar ferramentas, tratar requisições e conectar o servidor usando o Model Context Protocol.

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

### Exemplo Java: Componentes do Servidor MCP

Este exemplo demonstra o mesmo servidor MCP e registro de ferramentas do exemplo .NET acima, porém implementado em Java.

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
            
        // Registrar uma ferramenta de clima
        server.registerTool(McpToolDefinition.builder("weatherTool")
            .description("Gets current weather for a location")
            .parameter("location", String.class)
            .execute((ToolExecutionContext ctx) -> {
                String location = ctx.getParameter("location", String.class);
                
                // Obter dados climáticos (simplificado)
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
        
        // Conectar o servidor usando transporte stdio
        try (StdioServerTransport transport = new StdioServerTransport()) {
            server.connect(transport);
            System.out.println("Weather MCP Server started");
            // Manter o servidor em execução até o processo ser encerrado
            Thread.currentThread().join();
        }
    }
    
    private static WeatherData getWeatherData(String location) {
        // A implementação chamaria uma API de clima
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

### Exemplo Python: Construindo um Servidor MCP

Este exemplo usa fastmcp, então por favor certifique-se de instalá-lo antes:

```python
pip install fastmcp
```
Código de exemplo:

```python
#!/usr/bin/env python3
import asyncio
from fastmcp import FastMCP
from fastmcp.transports.stdio import serve_stdio

# Crie um servidor FastMCP
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

# Registrar ferramentas da classe
weather_tools = WeatherTools()

# Iniciar o servidor
if __name__ == "__main__":
    asyncio.run(serve_stdio(mcp))
```

### Exemplo JavaScript: Criando um Servidor MCP

Este exemplo mostra a criação de um servidor MCP em JavaScript e como registrar duas ferramentas relacionadas ao clima.

```javascript
// Usando o SDK oficial do Modelo de Protocolo de Contexto
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod"; // Para validação de parâmetros

// Criar um servidor MCP
const server = new McpServer({
  name: "Weather MCP Server",
  version: "1.0.0"
});

// Definir uma ferramenta de clima
server.tool(
  "weatherTool",
  {
    location: z.string().describe("The location to get weather for")
  },
  async ({ location }) => {
    // Normalmente isso chamaria uma API de clima
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
    // Normalmente isso chamaria uma API de clima
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

Este exemplo JavaScript demonstra como criar um servidor MCP que registra ferramentas ligadas a clima e se conecta usando transporte stdio para tratar requisições do cliente.

## Segurança e Autorização

O MCP inclui vários conceitos e mecanismos embutidos para gerenciar segurança e autorização ao longo do protocolo:

1. **Controle de Permissão de Ferramentas**:  
  Clientes podem especificar quais ferramentas um modelo pode usar durante uma sessão. Isso assegura que apenas ferramentas autorizadas explicitamente estejam acessíveis, reduzindo riscos de operações não intencionadas ou inseguras. Permissões podem ser configuradas dinamicamente com base em preferências do usuário, políticas organizacionais ou contexto da interação.

2. **Autenticação**:  
  Servidores podem exigir autenticação antes de permitir acesso a ferramentas, recursos ou operações sensíveis. Isso pode envolver chaves API, tokens OAuth ou outros esquemas de autenticação. Autenticação adequada garante que apenas clientes e usuários confiáveis possam invocar funcionalidades do servidor.

3. **Validação**:  
  Validação de parâmetros é aplicada para todas as invocações de ferramentas. Cada ferramenta define os tipos esperados, formatos e restrições para seus parâmetros, e o servidor valida as requisições de entrada de acordo. Isso previne que entradas malformadas ou maliciosas alcancem as implementações das ferramentas e ajuda a manter a integridade das operações.

4. **Limitação de Taxa (Rate Limiting)**:  
  Para evitar abusos e garantir uso justo dos recursos do servidor, MCP pode implementar limitação de taxa para chamadas de ferramentas e acesso a recursos. Limites podem ser aplicados por usuário, por sessão ou globalmente, ajudando a proteger contra ataques de negação de serviço ou consumo excessivo de recursos.

Combinando esses mecanismos, o MCP oferece uma base segura para integrar modelos de linguagem com ferramentas externas e fontes de dados, ao mesmo tempo que concede a usuários e desenvolvedores controle refinado sobre acesso e uso.

## Mensagens do Protocolo & Fluxo de Comunicação

A comunicação MCP usa mensagens estruturadas **JSON-RPC 2.0** para facilitar interações claras e confiáveis entre hosts, clientes e servidores. O protocolo define padrões específicos de mensagens para diferentes tipos de operação:

### Tipos de Mensagens Principais:

#### **Mensagens de Inicialização**
- Requisição **`initialize`**: Estabelece conexão e negocia versão do protocolo e capacidades
- Resposta **`initialize`**: Confirma recursos suportados e informações do servidor  
- **`notifications/initialized`**: Sinaliza que a inicialização foi concluída e a sessão está pronta

#### **Mensagens de Descoberta**
- Requisição **`tools/list`**: Descobre ferramentas disponíveis no servidor
- Requisição **`resources/list`**: Lista recursos disponíveis (fontes de dados)
- Requisição **`prompts/list`**: Recupera templates de prompt disponíveis

#### **Mensagens de Execução**  
- Requisição **`tools/call`**: Executa uma ferramenta específica com parâmetros fornecidos
- Requisição **`resources/read`**: Recupera conteúdo de um recurso específico
- Requisição **`prompts/get`**: Obtém um template de prompt com parâmetros opcionais

#### **Mensagens do Lado do Cliente**
- Requisição **`sampling/complete`**: O servidor solicita uma conclusão do LLM ao cliente
- **`elicitation/request`**: O servidor solicita entrada do usuário por meio do cliente
- Mensagens de Log: O servidor envia mensagens de log estruturadas ao cliente

#### **Mensagens de Notificação**
- **`notifications/tools/list_changed`**: O servidor notifica o cliente sobre mudanças nas ferramentas
- **`notifications/resources/list_changed`**: O servidor notifica o cliente sobre mudanças nos recursos  
- **`notifications/prompts/list_changed`**: O servidor notifica o cliente sobre mudanças nos prompts

### Estrutura da Mensagem:

Todas as mensagens MCP seguem o formato JSON-RPC 2.0 com:  
- **Mensagens de Requisição**: Incluem `id`, `method` e `params` opcionais  
- **Mensagens de Resposta**: Incluem `id` e `result` ou `error`  
- **Mensagens de Notificação**: Incluem `method` e `params` opcionais (sem `id` nem resposta esperada)

Essa comunicação estruturada assegura interações confiáveis, rastreáveis e extensíveis, suportando cenários avançados como atualizações em tempo real, encadeamento de ferramentas e gestão robusta de erros.

### Tasks (Experimental)

**Tasks** são um recurso experimental que fornece wrappers de execução duráveis, permitindo recuperação de resultados pós-processamento e acompanhamento de status para requisições MCP:

- **Operações de Longa Duração**: Acompanham cálculos caros, automação de workflows e processamento em lote
- **Resultados Diferidos**: Permitem polling do status da task e recuperação dos resultados quando completada
- **Acompanhamento de Status**: Monitoram o progresso da tarefa através dos estados definidos no ciclo de vida
- **Operações Multi-etapas**: Suportam workflows complexos que abrangem múltiplas interações

Tasks encapsulam requisições MCP padrão para permitir padrões de execução assíncrona para operações que não podem ser concluídas imediatamente.

## Principais Conclusões

- **Arquitetura**: MCP usa arquitetura cliente-servidor onde hosts gerenciam múltiplas conexões cliente para servidores
- **Participantes**: Ecosistema inclui hosts (aplicações de IA), clientes (conectores de protocolo) e servidores (provedores de capacidades)
- **Mecanismos de Transporte**: Comunicação suporta STDIO (local) e HTTP Streamable com SSE opcional (remoto)
- **Primitivas Centrais**: Servidores expõem ferramentas (funções executáveis), recursos (fontes de dados) e prompts (templates)
- **Primitivas do Cliente**: Servidores podem requisitar amostragem (compleções LLM com suporte a chamadas de ferramentas), elicitação (entrada do usuário incluindo modo URL), roots (limites do sistema de arquivos) e logging dos clientes
- **Recursos Experimentais**: Tasks fornecem wrappers duráveis para operações de longa duração
- **Base do Protocolo**: Construído sobre JSON-RPC 2.0 com versionamento baseado em data (atual: 2025-11-25)
- **Capacidades em Tempo Real**: Suporta notificações para atualizações dinâmicas e sincronização em tempo real
- **Segurança em Primeiro Lugar**: Consentimento explícito do usuário, proteção da privacidade e transporte seguro são requisitos centrais

## Exercício

Projete uma ferramenta MCP simples que seria útil no seu domínio. Defina:  
1. Qual seria o nome da ferramenta  
2. Quais parâmetros ela aceitaria  
3. Qual seria a saída retornada  
4. Como um modelo poderia usar essa ferramenta para resolver problemas do usuário


---

## O que vem a seguir

Próximo: [Capítulo 2: Segurança](../02-Security/README.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Aviso Legal**:
Este documento foi traduzido utilizando o serviço de tradução automática [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos para garantir a precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original em seu idioma nativo deve ser considerado a fonte autoritativa. Para informações críticas, recomenda-se a tradução profissional humana. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->