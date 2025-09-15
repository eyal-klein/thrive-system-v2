# 🐚 Empty Shell הראשון - Agent OS
## תוכנית יישום מפורטת

**תאריך:** 15 ספטמבר 2025  
**מטרה:** בניית Empty Shell Engine + Agent OS הראשון  
**גישה:** Bottom-up - מהבסיס למעלה  

---

## 🎯 התוכנית המלאה

### שלב 1: Empty Shell Engine (היום)
```yaml
empty_shell_engine:
  purpose: "המנוע הבסיסי ליצירת קונטיינרים ריקים"
  
  components:
    1_base_agent_class:
      file: "src/core/THRIVEAgent.ts"
      purpose: "הקלאס הבסיסי לכל הסוכנים"
      
    2_cassette_loader:
      file: "src/core/CassetteLoader.ts"
      purpose: "מנוע טעינת קסטות"
      
    3_empty_shell_service:
      file: "src/services/EmptyShellService.ts"
      purpose: "שירות יצירת וניהול Empty Shells"
      
    4_database_schema:
      file: "prisma/schema.prisma"
      purpose: "טבלאות לניהול סוכנים וקסטות"
```

### שלב 2: Agent OS Empty Shell (היום)
```yaml
agent_os_implementation:
  purpose: "Agent OS כ-Empty Shell ראשון"
  
  components:
    1_agent_os_class:
      file: "src/agents/AgentOS.ts"
      purpose: "Agent OS שיורש מ-THRIVEAgent"
      
    2_system_cassettes:
      folder: "cassettes/system/"
      purpose: "קסטות ניהול מערכת"
      
    3_management_api:
      file: "src/routes/agent-os.ts"
      purpose: "API endpoints לניהול Agent OS"
      
    4_dashboard_ui:
      file: "client/pages/AgentOS.tsx"
      purpose: "ממשק ניהול Agent OS"
```

### שלב 3: Basic Services (מחר)
```yaml
supporting_services:
  purpose: "השירותים שמזינים את Agent OS"
  
  components:
    1_cassette_management:
      purpose: "ניהול וחיפוש קסטות"
      
    2_llm_orchestration:
      purpose: "ניהול מרכזי של LLM APIs"
      
    3_voice_integration:
      purpose: "חיבור למערכת הקול"
      
    4_resource_manager:
      purpose: "ניהול משאבים ומדדים"
```

---

## 🛠️ שלב 1: Empty Shell Engine - יישום מפורט

### 1.1 THRIVEAgent Base Class
```typescript
// src/core/THRIVEAgent.ts
import { EventEmitter } from 'events';
import { CassetteLoader } from './CassetteLoader';
import { CoherenceMonitor } from './CoherenceMonitor';

export interface AgentConfig {
  agentId?: string;
  name: string;
  type: 'SYSTEM' | 'DYNAMIC' | 'NUCLEUS';
  role?: string;
  authority?: 'SUPREME' | 'HIGH' | 'MEDIUM' | 'BASIC';
  clientId?: string;
  dnaId?: string;
  microPrompt?: string;
}

export interface AgentDNA {
  clientId: string | null;
  dnaId: string | null;
  behavioral: Record<string, any>;
  declarative: Record<string, any>;
  emotional: Record<string, any>;
  coherenceTarget: number;
  currentCoherence: number;
}

export interface LoadedCassette {
  id: string;
  content: any;
  loadedAt: Date;
  priority: number;
}

export class THRIVEAgent extends EventEmitter {
  // Core Identity
  public readonly identity: {
    agentId: string;
    name: string;
    type: string;
    role: string;
    authority: string;
    created: Date;
    version: string;
  };

  // DNA Binding
  public dna: AgentDNA;

  // Empty Shell State
  public state: {
    status: 'INITIALIZING' | 'LOADING' | 'ACTIVE' | 'IDLE' | 'ERROR';
    health: number;
    lastActivity: Date | null;
    sessionId: string | null;
    context: Record<string, any>;
    memory: {
      shortTerm: any[];
      workingMemory: Record<string, any>;
      episodic: any[];
    };
  };

  // Cassette System
  public cassettes: {
    loaded: LoadedCassette[];
    available: string[];
    active: string | null;
    history: any[];
    cache: Map<string, any>;
  };

  // Capabilities (populated by cassettes)
  public capabilities: {
    actions: Map<string, Function>;
    knowledge: Map<string, any>;
    skills: Map<string, Function>;
    tools: Map<string, any>;
  };

  // Performance Metrics
  public metrics: {
    tasksExecuted: number;
    tasksSucceeded: number;
    tasksFailed: number;
    averageResponseTime: number;
    totalTokensUsed: number;
    coherenceHistory: any[];
    errorRate: number;
    uptime: number;
    lastCheck: Date;
  };

  private cassetteLoader: CassetteLoader;
  private coherenceMonitor: CoherenceMonitor;

  constructor(config: AgentConfig) {
    super();
    
    // Initialize identity
    this.identity = {
      agentId: config.agentId || `AGT-${Date.now()}`,
      name: config.name,
      type: config.type,
      role: config.role || 'executor',
      authority: config.authority || 'BASIC',
      created: new Date(),
      version: '1.0.0'
    };

    // Initialize DNA
    this.dna = {
      clientId: config.clientId || null,
      dnaId: config.dnaId || null,
      behavioral: {},
      declarative: {},
      emotional: {},
      coherenceTarget: 0.98,
      currentCoherence: 0.0
    };

    // Initialize empty state
    this.state = {
      status: 'INITIALIZING',
      health: 100,
      lastActivity: null,
      sessionId: null,
      context: {},
      memory: {
        shortTerm: [],
        workingMemory: {},
        episodic: []
      }
    };

    // Initialize empty cassette system
    this.cassettes = {
      loaded: [],
      available: [],
      active: null,
      history: [],
      cache: new Map()
    };

    // Initialize empty capabilities
    this.capabilities = {
      actions: new Map(),
      knowledge: new Map(),
      skills: new Map(),
      tools: new Map()
    };

    // Initialize metrics
    this.metrics = {
      tasksExecuted: 0,
      tasksSucceeded: 0,
      tasksFailed: 0,
      averageResponseTime: 0,
      totalTokensUsed: 0,
      coherenceHistory: [],
      errorRate: 0,
      uptime: 0,
      lastCheck: new Date()
    };

    // Initialize services
    this.cassetteLoader = new CassetteLoader(this);
    this.coherenceMonitor = new CoherenceMonitor(this);
  }

  /**
   * Initialize the Empty Shell
   */
  async initialize(): Promise<{ success: boolean; agentId: string }> {
    try {
      this.log('INFO', 'Initializing Empty Shell...');
      
      // Step 1: Load micro-prompt (if provided)
      if (this.dna.dnaId) {
        await this.loadMicroPrompt();
      }
      
      // Step 2: Load mandatory governance cassettes
      await this.loadMandatoryCassettes();
      
      // Step 3: Validate coherence
      await this.validateCoherence();
      
      // Step 4: Connect to THRIVE system
      await this.connectToSystem();
      
      // Step 5: Start monitoring
      this.startMonitoring();
      
      this.state.status = 'ACTIVE';
      this.log('INFO', 'Empty Shell initialized successfully');
      
      this.emit('initialized', { agentId: this.identity.agentId });
      
      return { success: true, agentId: this.identity.agentId };
      
    } catch (error) {
      this.state.status = 'ERROR';
      this.log('ERROR', `Initialization failed: ${error.message}`);
      throw error;
    }
  }

  /**
   * Load a cassette into the agent
   */
  async loadCassette(cassetteId: string, options: { priority?: number } = {}): Promise<void> {
    return this.cassetteLoader.load(cassetteId, options);
  }

  /**
   * Unload a cassette
   */
  async unloadCassette(cassetteId: string): Promise<void> {
    return this.cassetteLoader.unload(cassetteId);
  }

  /**
   * Execute a task using loaded capabilities
   */
  async executeTask(task: any): Promise<any> {
    const startTime = Date.now();
    
    try {
      this.state.status = 'EXECUTING';
      this.log('INFO', `Executing task: ${task.id || 'unnamed'}`);
      
      // Find appropriate capability
      const capability = this.findCapability(task.type);
      
      if (!capability) {
        throw new Error(`No capability for task type: ${task.type}`);
      }
      
      // Execute capability
      const result = await capability({
        task,
        context: this.state.context,
        dna: this.dna,
        memory: this.state.memory
      });
      
      // Update metrics
      this.updateMetrics(startTime, true);
      
      this.state.status = 'ACTIVE';
      return result;
      
    } catch (error) {
      this.updateMetrics(startTime, false);
      this.state.status = 'ERROR';
      this.log('ERROR', `Task execution failed: ${error.message}`);
      throw error;
    }
  }

  /**
   * Get agent status
   */
  getStatus(): any {
    return {
      identity: this.identity,
      dna: this.dna,
      state: this.state,
      cassettes: {
        loaded: this.cassettes.loaded.length,
        active: this.cassettes.active
      },
      capabilities: {
        actions: this.capabilities.actions.size,
        knowledge: this.capabilities.knowledge.size,
        skills: this.capabilities.skills.size,
        tools: this.capabilities.tools.size
      },
      metrics: this.metrics
    };
  }

  // Private methods
  private async loadMicroPrompt(): Promise<void> {
    // Implementation for loading micro-prompt
  }

  private async loadMandatoryCassettes(): Promise<void> {
    const mandatory = [
      'META.1.001', // System Architecture
      'META.1.003', // Agent Template Framework
      'META.5.001', // Coherence Algorithm
      'CORE.COHERENCE.001' // Coherence Monitor
    ];
    
    for (const cassetteId of mandatory) {
      await this.loadCassette(cassetteId);
    }
  }

  private async validateCoherence(): Promise<void> {
    const coherence = await this.coherenceMonitor.calculate();
    if (coherence < this.dna.coherenceTarget) {
      throw new Error(`Coherence validation failed: ${coherence}`);
    }
  }

  private async connectToSystem(): Promise<void> {
    // Implementation for system connection
  }

  private startMonitoring(): void {
    // Implementation for monitoring loops
  }

  private findCapability(taskType: string): Function | null {
    return this.capabilities.actions.get(taskType) || null;
  }

  private updateMetrics(startTime: number, success: boolean): void {
    const duration = Date.now() - startTime;
    
    this.metrics.tasksExecuted++;
    if (success) {
      this.metrics.tasksSucceeded++;
    } else {
      this.metrics.tasksFailed++;
    }
    
    this.metrics.averageResponseTime = 
      (this.metrics.averageResponseTime + duration) / 2;
    
    this.metrics.errorRate = 
      this.metrics.tasksFailed / this.metrics.tasksExecuted;
    
    this.metrics.lastCheck = new Date();
  }

  private log(level: string, message: string): void {
    console.log(`[${level}] ${this.identity.agentId}: ${message}`);
    // TODO: Implement proper logging system
  }
}
```

### 1.2 CassetteLoader Service
```typescript
// src/core/CassetteLoader.ts
import { THRIVEAgent, LoadedCassette } from './THRIVEAgent';

export class CassetteLoader {
  constructor(private agent: THRIVEAgent) {}

  async load(cassetteId: string, options: { priority?: number } = {}): Promise<void> {
    try {
      // Check if already loaded
      if (this.agent.cassettes.loaded.find(c => c.id === cassetteId)) {
        this.agent.log('WARN', `Cassette already loaded: ${cassetteId}`);
        return;
      }

      // Fetch cassette from vault/academy
      const cassette = await this.fetchCassette(cassetteId);
      
      // Validate cassette
      this.validateCassette(cassette);
      
      // Load cassette content
      const loadedCassette: LoadedCassette = {
        id: cassetteId,
        content: cassette,
        loadedAt: new Date(),
        priority: options.priority || 10
      };
      
      this.agent.cassettes.loaded.push(loadedCassette);
      
      // Extract and register capabilities
      this.extractCapabilities(cassette);
      
      this.agent.log('INFO', `Cassette loaded: ${cassetteId}`);
      
    } catch (error) {
      this.agent.log('ERROR', `Failed to load cassette: ${error.message}`);
      throw error;
    }
  }

  async unload(cassetteId: string): Promise<void> {
    const index = this.agent.cassettes.loaded.findIndex(c => c.id === cassetteId);
    if (index === -1) {
      throw new Error(`Cassette not loaded: ${cassetteId}`);
    }
    
    const cassette = this.agent.cassettes.loaded.splice(index, 1)[0];
    
    // Remove capabilities
    this.removeCapabilities(cassette.content);
    
    this.agent.log('INFO', `Cassette unloaded: ${cassetteId}`);
  }

  private async fetchCassette(cassetteId: string): Promise<any> {
    // Implementation for fetching cassette from vault/academy
    const response = await fetch(`/api/vault/cassettes/${cassetteId}`);
    if (!response.ok) {
      throw new Error(`Failed to fetch cassette: ${cassetteId}`);
    }
    return response.json();
  }

  private validateCassette(cassette: any): void {
    // Implementation for cassette validation
    if (!cassette.id || !cassette.content) {
      throw new Error('Invalid cassette format');
    }
  }

  private extractCapabilities(cassette: any): void {
    // Implementation for extracting capabilities from cassette
    if (cassette.capabilities) {
      // Register actions
      if (cassette.capabilities.actions) {
        for (const [name, action] of Object.entries(cassette.capabilities.actions)) {
          this.agent.capabilities.actions.set(name, action as Function);
        }
      }
      
      // Register knowledge
      if (cassette.capabilities.knowledge) {
        for (const [domain, knowledge] of Object.entries(cassette.capabilities.knowledge)) {
          this.agent.capabilities.knowledge.set(domain, knowledge);
        }
      }
      
      // Register skills
      if (cassette.capabilities.skills) {
        for (const [name, skill] of Object.entries(cassette.capabilities.skills)) {
          this.agent.capabilities.skills.set(name, skill as Function);
        }
      }
      
      // Register tools
      if (cassette.capabilities.tools) {
        for (const [name, tool] of Object.entries(cassette.capabilities.tools)) {
          this.agent.capabilities.tools.set(name, tool);
        }
      }
    }
  }

  private removeCapabilities(cassette: any): void {
    // Implementation for removing capabilities
    if (cassette.capabilities) {
      if (cassette.capabilities.actions) {
        for (const name of Object.keys(cassette.capabilities.actions)) {
          this.agent.capabilities.actions.delete(name);
        }
      }
      // Similar for other capability types...
    }
  }
}
```

### 1.3 Database Schema Updates
```prisma
// prisma/schema.prisma - הוספות לסכמה הקיימת

model Agent {
  id                String   @id @default(cuid())
  agentId           String   @unique
  name              String
  type              String   // SYSTEM, DYNAMIC, NUCLEUS
  role              String
  authority         String
  clientId          String?
  dnaId             String?
  status            String   @default("INITIALIZING")
  health            Int      @default(100)
  coherenceTarget   Float    @default(0.98)
  currentCoherence  Float    @default(0.0)
  configuration     Json     @default("{}")
  metrics           Json     @default("{}")
  createdAt         DateTime @default(now())
  updatedAt         DateTime @updatedAt
  
  // Relations
  loadedCassettes   AgentCassette[]
  
  @@map("agents")
}

model Cassette {
  id              String   @id @default(cuid())
  cassetteId      String   @unique
  name            String
  category        String
  classification  String   @default("RESTRICTED")
  version         String   @default("1.0.0")
  content         Json
  capabilities    Json     @default("{}")
  dependencies    String[] @default([])
  coherenceScore  Float    @default(0.0)
  size            Int      @default(0)
  checksum        String?
  createdAt       DateTime @default(now())
  updatedAt       DateTime @updatedAt
  
  // Relations
  loadedBy        AgentCassette[]
  
  @@map("cassettes")
}

model AgentCassette {
  id          String   @id @default(cuid())
  agentId     String
  cassetteId  String
  priority    Int      @default(10)
  loadedAt    DateTime @default(now())
  active      Boolean  @default(false)
  
  // Relations
  agent       Agent    @relation(fields: [agentId], references: [agentId])
  cassette    Cassette @relation(fields: [cassetteId], references: [cassetteId])
  
  @@unique([agentId, cassetteId])
  @@map("agent_cassettes")
}

model EmptyShell {
  id            String   @id @default(cuid())
  templateId    String   @unique
  name          String
  description   String?
  baseConfig    Json     @default("{}")
  mandatoryCassettes String[] @default([])
  version       String   @default("1.0.0")
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  
  @@map("empty_shells")
}
```

---

## 🚀 משימה ראשונה לאייג'נט התכנות

**אני רוצה שתתחיל עם יצירת Empty Shell Engine:**

### שלב 1.1: יצירת המבנה הבסיסי
```yaml
tasks:
  1. "צור תיקייה src/core/"
  2. "צור קובץ src/core/THRIVEAgent.ts עם הקלאס הבסיסי"
  3. "צור קובץ src/core/CassetteLoader.ts"
  4. "צור קובץ src/core/CoherenceMonitor.ts (stub בינתיים)"
  5. "עדכן את prisma/schema.prisma עם הטבלאות החדשות"
```

### שלב 1.2: יצירת Empty Shell Service
```yaml
tasks:
  1. "צור src/services/EmptyShellService.ts"
  2. "צור src/routes/empty-shell.ts עם API endpoints"
  3. "הוסף את הroutes ל-index-fastify.js"
  4. "צור בדיקות בסיסיות"
```

### שלב 1.3: בדיקה ראשונית
```yaml
tasks:
  1. "הרץ npx prisma generate"
  2. "הרץ npx prisma db push"
  3. "בדוק שהשירות עולה"
  4. "בדוק יצירת Empty Shell בסיסי"
```

**מוכן להתחיל עם שלב 1.1?**

