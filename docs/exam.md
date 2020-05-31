
## PSS d. 4/6
[Form](https://www.moodle.aau.dk/mod/page/view.php?id=1057193)
[Topic](https://www.moodle.aau.dk/mod/page/view.php?id=1060645)
- 28/5
  - **Processes and Threads**
    - Definition of process/thread (why do we need processes?)
      - Process &rarr; A running program.
        - Limited access to cpu and I/O
        - Er i forskellige stadier **machine state**
          - memory &rarr; skrive / læse
          - registre &rarr; læse og opdatere registre
          - I/O &rarr; tilgår andre enheder | harddisk, mus, tastatur, usb
        - An illusion (virtualization) of a CPU
      - Thred &rarr; 

    - process-/threadcontrol block (how are processes/threads implemented in the OS?)

      - Process technique = **time sharing**
      - low-level machinery = **mechanisms**
        -  Low level protocols / functions
      - `API`
        - `CREATE`
        - `DESTROY`
        - `WAIT` til en process er færdig med at køre
        - `Miscellaneous Control`: kunne fx være at suspendere et process it et stykke tid, for at den skal køre videre bagefter
        - `Status`: hvor lang tid har en process kørt, hvilket stadie er den i?

    - 5-state process model (what is the lifecycle of a process?) 

      - New: processen er ikke blevet indlæst i hukommelsen endnu  
      - Ready: processen er klar til køre instruktioner
      - Running: Kører intruktioner 
      - Blocked: venter på et event (evt i/o eller netværks pakke)
      - Exit: frigivet fra hukommelsen 

    - process creation 

      1. Indlæs kode  og statiske date (initialiserede variable) fra harddisk ind i hukommelsen
         - moderne os bruger lazy loading og indlæser kun nødvendige sider (memory pages)
      2. Allokere plads til stakken
         - intialisere `argc` og `argv` med input fra terminalen
      3. Allokere plads til heapen
      4. Forbinder I/O til processen - fx hvor printf skal skrive til
      5. Kør entrypoint i programmet (fx kør main i C)

    - process/thread switching

      - **process list** relevant info om alle kørende processor &darr; `XV6`

        De er meget komplexe i rigtige OS.

        - **register context**: indholdet på en proces
        - 

      - **scheduling policy** hvilket program skal kører først

      - en **context switch** som stopper et program, for at køre et andet | **mechanism**

    - multi-threading

    - implementation strategies for thread support

    - user-/kernel-/hybrid-mode (what are the pros and cons of of the different approaches?)

- 29/5
  - **Scheduling**
    - Definition of scheduler (what is a scheduler? why do we need a scheduler?)
    - Metrics for scheduling: fairness, turnaround time, response time (what is a good scheduler?)
    - simple process model
    - scheduling policies (FIFO, SJF, STCF, Round Robin, MLFQ, lottery scheduler)

- 30/5
  - **Memory management**
    - *Memory hierarchy (why don’t we just use registers for everything?)*
    - *goals for memory management (transparency, efficiency, isolation)*
	    - Transperant (interface for programmøre)
		    - En abstraction, så man ved der sker, men ikke hvordan det sker
		    - Opnåes ved at man ikke skal tænke på fysiske adresser
	    - Effektivt
		    - Hukommelsen bliver brugt hele tiden, så det skal være hurtigt, da det har stor indflydelse på systemes oplevelse. (alt ville være langsomt)
		    - Opnåes med MMU
	    - Beskyttelse
		    - Så process a ikke læser eller skriver til process b. Hvis der lå et password eller api nøgle i process b.  
		    - Så ingen process gør ændre noget ved OS. "jeg skal køre i kernal mode"
		    - Det opnåes ved isolation
	    - Hvis der ikke var nogle håndtering, skulle vi skrive proces a til hardisken, for at derfter at læse proces b. Det er ineffektivt
	    - 
    - *address space (what is an address space? why do we need that abstraction?)*
	    - hvordan hukommelsen er lagt ud for processen kan bruge
	 - *virtual memory (what exactly is virtual memory?)*
		 - En abstraction til at gøre humkommelsen pæn
		 - Kør det pænt for programmøren
		 - Kan bruge swap hukommelsen, så man udvider hukommelsen
		 - Forventninger:
			 - sammenhængende tildeling
			 - Småt adresse rum
			 - låst størrelse på tildeling
    - *challenges for memory management*
	    - Hvordan man bruger alt hukommelsen. Fx hvis der er free space mellem proc a og proc b
	    - Så kan vi have 2 programmer i hukommelsen
    - *features (relocation, protection, and sharing)*
    - *virtual addresses vs. physical addresses (why do we need virtual addresses? how can we translate a virtual address to a physical address?)*
	    - virtuelle ease of use til programmøre
	    - det er en abstraction/API på hukommelses adresses
	    - Sikkerhed, vi skal undgå at et program ikke kigger på andre programmer
    - *address translation*
	    - va + BASE register = fysisk adresse
	    - er fysisk adresse mindre end BOUND og større end BASE? ok ,ellers error/kill 
	    - Det sker på MMU (memory manage unit)
	    - effektivt fordi det sker på hardware niveau
    - *segmentation (what problem does it solve? how is it implemented? what are the problems with segmentation?)*
	    - Der kan være spild plads, i den allokeret blok. (fx der er meget plads mellem heapen og stakken)
	    - tre segmenter:
		    - kode segment
		    - heap segment
		    - stak segment
	    - løses med base bound til hver segment (3 par her)
	    - fys adresse = OFFSET(virtual base) + BASE
	    - fys adresse  =va + vbase + BASE
	    - trick:
		    - code = 00
		    - heap = 01
		    - stak = 11
    - *base and bound registers (what are they? how do they work? why do they work?)*
	    - base | va 0 = fysisk start adresse
	    - bound | va max = fysisk slut adresse
		    - Sikre at vi ikke skriver til noget udenfor vores stykke hukommelse
    - *simple allocation*
    - *dynamic allocation*

- 31/5
  - **Paged memory**
    - Address types (physical, relative, virtual)
    - Pages and frames (what are they? where do they reside? how big are they typically?)
    - address translation
    - page tables (what are they? how many are there? what are they used for? how are they used?)
    - virtual memory, swapping, shared memory (why is that easy with paged memory?)
    - page replacement algorithms (OPT, LRU, FIFO, CLOCK)

- 1/6
  - **Concurrency**
    - Multi-threading (what is that? why would we want that?)
    - implementation strategies for multi-threading (how is it implemented? what are the tradeoffs os the different implementation approaches?)
    - concurrency vs. parallelism (what is the difference? why is it important?)
    - inter-process communication
    - race conditions (what are they? is it a problem?)
    - mutual exclusion (why would we want that?)
    - ensuring mutual exclusion (algorithms, hardware supported, mutexes, semaphores, monitors)

- 2/6
  - **Concurrency problems**
    - Definition of deadlock (what is it? is it a real problem?)
    - Mutual exclusion (what is it? why do we want that?)
    - Resource allocation graph (what is it? how to make one? why can we use it for?)
    - Coffman’s conditions
    - Solution strategies (prevention, avoidance, detection and recovery)
    - How to achieve deadlock prevention (breaking Coffman’s conditions)
    - Safe states and deadlock avoidance
    - Deadlock detection and recovery, livelock, priority inversion.
  
- 3/6
  - **XV6 Process switching**
    - XV6 components involved in process swithcing (what files are involved?
what functions are involved? what parts of the OS are involved?)
    - challenges (how is user-space/kernel-space switch handled? how/when is a process de-scheduled?)

## SPO 08/6
[Link to moodle](https://www.moodle.aau.dk/course/view.php?id=33042)

1. Language Design Sequence control and Subprogram Control
    - Language Design Criteria
    - Evaluation of expressions
    - Explicit sequence control vs. structured sequence control
    - Loop constructs
    - Subprogram
    - Parameter mechanisms

2. Structure of the compiler
    - Describe the phases of the compiler and give an overall description of what the purpose of each phase is and how the phases interface
    - Single pass vs. multi pass compiler
      - Issues in language design
      - Issues in code generation
3. Lexical analysis
    - Describe the role of the lexical analysis phase
    - Describe how a scanner can be implemented by hand or auto-generated
    - Describe regular expressions and finite automata
4. Parsing
    - Describe the purpose of the parser
    - Discuss top down vs. bottom up parsing
    - Explain necessary conditions for construction of recursive decent parsers
    - Discuss the construction of an RD parser from a grammar
    - Discuss bottom Up/LR parsing
5. Semantic Analysis
    - Describe the purpose of the Semantic analysis phase
    - Discuss Identification and type checking
    - Discuss scopes/block structure and implication for implementation of identification tables/symbol tables
    - Discuss Implementation of semantic analysis
6. Run-time organization
    - Data representation (direct vs. indirect)
    - Storage allocation strategies: static vs. stack dynamic
    - Activation records (sometimes called frames)
    - Routines and Parameter passing
7. Heap allocation and Garbage Collection
    - Why may we need heap allocation?
    - Garbage collection strategies (Types of GCs)
8. Code Generation
    - Describe the purpose of the code generator
    - Discuss Intermediate representations
    - Describe issues in code generation
    - Code templates and implementations
    - Back patching
    - Implementation of functions/procedures/methods
    - Register Allocation and Code Scheduling
## SS 12/6
[Link to moodle](https://www.moodle.aau.dk/course/view.php?id=33046)

**Generelt**
- 5 Opgaver
- 2 sider pr opgave -> 10 sider i alt
- 
