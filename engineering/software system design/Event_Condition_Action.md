# Event-driven model: Event-Condition-Action

[TOC]

## ECA Basic Model

> **WHEN**  <*event*>  **IF**  <*condition*>  **THEN**  <*action*>.

The event-driven model is a architecture paradigm that places events at its core. Its central idea is that the occurrence of events drives the program’s execution flow, rather than relying on traditional sequential control flow. In this model, the system’s behavior revolves around event generation, detection, dispatch, and handling, thereby enabling a highly decoupled, asynchronous, and reactive system design.

- **Events**: A detectable occurrence, which carries the attribute parameters and type of the event, and defines specific events or signals that can cause a change in the system state or require a system response. It is the starting point of the entire model’s execution and may originate from external inputs (such as user clicks), internal state changes (such as data updates), or time-based conditions (such as a timer expiring).
- **Conditions**: After the event is triggered, this consists of the logical rules or preconditions used to determine whether the corresponding action should be executed. The execution prerequisites ensure that subsequent actions are performed only when specific conditions are met.
- **Actions**: The concrete operations or behaviors performed by the model when the event occurs and the conditions are satisfied. It represents the final realization of event handling and may include updating data, invoking services, granting rewards, sending messages, or triggering new events, thereby completing a full event-response cycle.

![ECA](assets/ECA.svg)

### Events Triggering

#### Attributes

**Attributes** are data fields carried by a specific business event, containing explicit business information. When an identifiable event occurs in the system (such as “user login” or “order payment success”), the event object is not merely a signal—it is a data packet. The various pieces of information contained in this packet are the event attributes. These attributes give the event concrete business meaning, transforming it from an abstract notification into a contextual object that can be used for logical decisions and business processing.

**Which Events can be combined with which Conditions and Actions?** Each Event, when fired, provides a set of event attributes carrying specific business information (e.g., user ID, order amount). Each Condition and Action, in turn, declares the set of attributes it requires for execution (for example, “check amount” requires order amount; “grant reward” requires user ID). The system automatically determines whether a combination is valid and executable by checking whether the attributes provided by the Event satisfy the requirements of the Condition and Action. This mechanism allows Events, Conditions, and Actions to automatically adapt based on their data interfaces, supporting a flexible, reliable, and dynamically configurable business rules system.

1. **Schema Matching.** Each event defines an output schema, while a condition or action defines an input schema. The system compares the Event’s output schema with the required input schemas of the selected Conditions and Actions. A composition is considered valid only when all required attributes can be resolved from the Event attributes or other explicitly declared data sources.
2. **Type Checking.** It verifies whether the attributes used by conditions and actions have compatible data types. Meanwhile, a robust ECA system should validate not only primitive types, but also semantic types. This avoids accidental misuse of fields that share the same primitive type but represent different business concepts.
3. **Data Contract Validation.** It helps ensure that the schema evolution of event/condition/action do not silently break existing rule configurations (schema is part of data contract), and ensure the system must verify existing rules remain compatible. Therefore, each event/condition/action should be versioned, while rule configurations should reference specific schema versions to ensure deterministic execution.

**Consistency issues in data dependencies between Events and Conditions**. Events may indicate the occurrence of a “local event” within the system, whereas Condition evaluation requires the “global state to be ready.” The essence of the problem lies in the temporal misalignment between the “local event” and the “global state readiness”: when a event occurs, other related data required for subsequent condition evaluation may not yet have been generated, persisted, or may still be in an inconsistent intermediate state. Because different system components process data at different speeds, a time gap emerges between cross-component state consistency and the requirements of business logic. Therefore, the key to system design is to clearly identify and define the true business moment at which “all required data are ready and consistent,” and to use that moment as a reliable triggering signal.

#### Special Events: Runtime Events

Because an ECA Graph is not only driven by external business events, but also by internal runtime state changes, some special events are necessary. Multiple ECA Nodes are composed into a DAG, the runtime must react to internal execution milestones, such as a predecessor node being completed, a dependency being satisfied, a branch being selected, or an asynchronous action callback being received. Without Special Events, these internal transitions would have to be implemented as implicit control logic inside the scheduler. By representing important runtime changes as explicit events, the system can treat internal graph progression in the same event-driven manner as external business triggers.

Special Events can be used to drive the transition of an ECA Graph from one node to its successor nodes. When an upstream ECA Node completes, the runtime emits a lifecycle event such as `NodeCompleted`. This event does not only indicate that the node has reached a terminal state; it can also carry the business data produced or consumed by that node, so that downstream nodes can use the data during their own condition evaluation and action execution. This mechanism allows the ECA Graph to support data propagation between nodes without relying on hidden control flow. Each transition is represented by an explicit event, and each downstream node receives a well-defined input context derived from upstream execution results.



| Special Event           | Triggered When                                               | Runtime Semantics                                            | Typical Use Case                                             |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `GraphInstantiated`     | A Meta ECA Graph is instantiated into a runtime execution instance. | Marks the creation of a new executable graph instance.       | Initialize graph context, create node instances, assign idempotency keys. |
| `GraphStarted`          | A graph instance begins execution.                           | Indicates that the graph is ready to evaluate its initial executable nodes. | Start source ECAs or compute the initial frontier node set.  |
| `NodeReady`             | A node’s upstream dependency conditions are satisfied.       | Moves a node from `Pending` to `Ready`.                      | Enable a successor node after all required parent nodes are completed. |
| `NodeStarted`           | A ready node is selected for execution.                      | Marks the beginning of condition evaluation and action execution for a node. | Track node execution lifecycle and prevent duplicate execution. |
| `NodeCompleted`         | A node successfully finishes its condition evaluation and action execution. | The most common internal event for directly triggering downstream nodes. | Automatically activate successor nodes after a predecessor node completes. |
| `NodeSkipped`           | A node is intentionally skipped because its condition is not satisfied or its branch is not selected. | Marks the node as non-executable without treating it as a failure. | Continue graph execution when a node is optional or conditionally bypassed. |
| `NodeInvalidated`       | A node becomes invalid due to branch exclusion or graph-level control logic. | Prevents the node from being executed in the current graph instance. | Implement mutual exclusion between sibling branches.         |
| `NodeFailed`            | A node fails during condition evaluation or action execution. | Marks the node as failed and triggers retry, compensation, or graph failure policy. | Handle rule evaluation errors, action failures, or external service errors. |
| `NodeTimedOut`          | A node or its asynchronous action does not complete within the configured timeout. | Converts long-running or unresolved execution into a controlled timeout event. | Trigger retry, mark failure, or continue with fallback logic. |
| `DependencySatisfied`   | The required parent-node transition condition is satisfied.  | Indicates that a child node can become ready based on `AND`, `OR`, or `M-of-N` dependency rules. | Decouple dependency calculation from actual node execution.  |
| `JoinSatisfied`         | A join node receives enough completed upstream branches to proceed. | Resolves convergence semantics for multiple upstream paths.  | Start a downstream node after all or some parallel branches complete. |
| `BranchSelected`        | One branch among multiple candidate branches is selected.    | Commits the graph to a specific branch.                      | Implement exclusive branching, such as choosing one reward path among many. |
| `BranchInvalidated`     | Non-selected sibling branches are invalidated after a branch is selected. | Closes mutually exclusive paths that should no longer be executable. | Prevent duplicate rewards or conflicting actions across sibling branches. |
| `ActionSubmitted`       | An action is sent to an internal or external executor.       | Marks that the action has been dispatched but may not have completed yet. | Track asynchronous actions and correlate callbacks.          |
| `ActionCompleted`       | A synchronous action returns successfully or an asynchronous callback confirms success. | Confirms that the action side effect has succeeded.          | Allow the node to complete and trigger downstream ECAs.      |
| `ActionFailed`          | An action fails synchronously or an asynchronous callback reports failure. | Converts action failure into a node-level failure or retry decision. | Trigger retry, compensation, fallback, or graph failure.     |
| `CallbackReceived`      | An external system sends a callback for a previously submitted asynchronous action. | Resumes a paused node or action execution.                   | Continue graph execution after payment confirmation, reward issuance, or third-party approval. |
| `RetryScheduled`        | A failed or timed-out node/action is scheduled for another attempt. | Defers execution according to retry policy.                  | Handle transient failures without immediately failing the graph. |
| `CompensationRequested` | A completed side effect must be reversed because a later step failed. | Starts a compensating action for already completed effects.  | Support Saga-like rollback semantics.                        |
| `RoundStarted`          | A new execution round begins for the same graph and instance key. | Separates repeated business executions under the same logical entity. | Support multi-round campaigns, repeated tasks, or recurring reward flows. |
| `RoundCompleted`        | All executable nodes in the current round reach a terminal state. | Marks the end of one execution round.                        | Determine whether another round can start or the graph should terminate. |
| `GraphCompleted`        | All required paths in the graph instance are completed, skipped, or invalidated according to graph completion policy. | Marks the graph instance as successfully completed.          | Emit final strategy result, persist execution summary, notify downstream systems. |
| `GraphFailed`           | The graph can no longer proceed due to unrecoverable node failure, timeout, or policy violation. | Marks the graph instance as failed.                          | Trigger alerting, manual intervention, compensation, or failure reporting. |

### Conditions Evaluation

**Conditions** are the decision-making component of an ECA Node, to determine whether the action is eligible to run. In a configurable strategy system, conditions are usually represented by a structured rule expression or a domain-specific language (DSL). This allows business rules to be configured and executed dynamically without changing application code.

At the most basic level, a condition describes a predicate over event attributes, runtime context, and business state. A condition expression is usually composed of several fundamental elements:

1. **Operands.** Operands are the values participating in the condition expression. They may come from event attributes, graph context, entity state, external systems, or static configuration.
2. **Operators.** Operators define how operands are compared or combined.
3. **Logical Connectors.** Multiple predicates can be combined into a compound condition using logical connectors.
4. **Functions.** A condition DSL may also support built-in or custom functions for common business logic. Functions should be carefully controlled because they may introduce external dependencies, non-deterministic behavior, or performance costs.
5. **Aggregations.** Some conditions require aggregation over a collection or time window. Aggregation conditions are more complex than simple predicates because they depend on historical data, time windows, and consistency guarantees.
6. **Quantifiers.** For collection-based data, the DSL may support quantifiers such as `any`, `all`, or `none`. These allow the condition system to express rules over lists, sets, and related entities.

**Atomic vs. Composite.** A condition can be either atomic or composite. An **atomic condition** is the smallest independently evaluable predicate. A **composite condition** is composed of multiple atomic conditions connected by logical operators. This distinction is important because the rule engine may evaluate, trace, optimize, or short-circuit each atomic condition independently.

#### Condition Lifecycle

The full lifecycle from rule-template configuration to final resolution of rules is a process of progressively aggregating information and refining conditions.

1. **Condition Definition**. A condition is usually defined from a reusable condition template. The template describes the logical structure of the condition, the required input attributes, supported operators, and configurable parameters. At this stage, the condition is still abstract. It does not yet contain the concrete threshold value, event data, or runtime state required for execution.

2. **Condition binding.** After the strategy is configured, the system binds the condition template with static configuration values to produce a concrete condition definition. Condition binding converts reusable templates into strategy-specific rules. This stage also allows the system to validate whether the required attributes of the condition can be provided by the triggering event, graph context, or external data source. If the condition requires an attribute that cannot be resolved, the ECA Node should be considered invalid during configuration validation rather than failing at runtime.

3. **Context Resolution.** When an event triggers an ECA Node, the system builds an evaluation context for the condition. The evaluation context is the complete data environment used by the rule engine to evaluate the condition. This stage is critical because an event may only represent a local occurrence, while condition evaluation may require a globally consistent business state. Therefore, the system must clearly define which business moment should be treated as the reliable point for evaluation. If the required state is not ready, the node should either wait, retry, or be triggered by a later state-ready event.
4. **Expression Compilation.** Before evaluation, the bound condition is translated into an executable internal representation. Depending on the implementation of the rule engine, this representation may be an abstract syntax tree, bytecode, decision table, predicate chain, or another optimized structure. Compilation separates rule authoring from rule execution. It allows condition definitions to be validated before runtime and enables the runtime engine to evaluate conditions efficiently and deterministically.
5. **Condition Evaluation.** The rule engine evaluates the compiled condition against the resolved context and produces an evaluation result. In a complex strategy system, the evaluation result should also include structured metadata that explains how the decision was made. This makes condition evaluation observable and explainable, which is especially important for business rules, rewards, risk control, and financial operations.
6. **Result Emission.** After evaluation, the ECA runtime uses the condition result to determine the next state of the ECA Node. The result may also be written back to the graph context so that downstream ECA Nodes can consume it during their own condition evaluation. In this way, condition evaluation is not merely a local boolean check. It is a structured decision process that connects rule configuration, event data, runtime state, external dependencies, and graph-level execution control.

**System**: Starting from a predefined condition template and static configuration, the system produces a set of baseline conditions that form the foundational framework. It then enriches these baseline conditions with dynamic contextual information to derive the final, complete condition set.

**Rule Engine**: Rule Engine performs the final condition evaluation and emit resolution results.. Taking the complete condition as input and incorporating external system data (for example, payment status from third-party systems), it translates the condition into an executable internal representation (e.g., an abstract syntax tree and symbol table) that the rule engine can interpret. The engine then evaluates the logic and returns the result (decision, flags, or computed outputs).

![condition](./assets/condition.svg)

### Action Execution

After the Condition of an ECA Node is evaluated as satisfied, the runtime enters the Action Execution phase. An Action represents the concrete side effect or business operation produced by the ECA Node. When an ECA Node contains multiple actions, the runtime may support different execution strategies depending on the dependencies among actions. Actions can be executed in three common modes:

- **Sequential Execution**: Actions are executed one after another according to their configured order. This mode is used when a later action depends on the output or side effect of a previous action.
- **Parallel Execution**: Multiple actions are executed concurrently when they are independent and do not depend on each other’s outputs. The ECA Node proceeds only after all required parallel actions have reached their expected terminal states.
- **DAG-based Execution**: Actions are organized as an internal directed acyclic graph, where edges represent data dependencies, side-effect dependencies, or execution ordering constraints. This allows the node to combine sequential and parallel execution within the same action plan.


When multiple actions are executed sequentially, the processing mechanism operates in two distinct modes:

- **Synchronous Action**: A synchronous action completes within the current execution context. Its result is immediately available to the runtime, allowing the system to persist the action result, update the ECA node status, and continue scheduling downstream ECA nodes without waiting for an external signal.
- **Asynchronous Action**: An asynchronous action is submitted during the current execution context, but its final result is not immediately available. The action usually depends on an external system, long-running task, or delayed business process. After submission, the ECA Node enters a waiting state. The runtime resumes the node only after receiving a correlated completion event, callback, or timeout signal.

![202505252226](./assets/202505252226.svg)

**Idempotency.** Because actions often produce side effects, every action execution should be protected by an idempotency mechanism. This is especially important when the system receives duplicate events, retries failed operations, or processes duplicate callbacks from external systems. The runtime should ensure that the same logical action is executed only once for the same business context. If a duplicate execution request is received, the system should return the previously persisted result instead of performing the side effect again.

**Output Propagation.** An action may produce structured outputs that are written into the execution context of the current ECA Node or the broader ECA Graph instance. These outputs can be used by: subsequent actions within the same ECA node, downstream ECA nodes in the graph, condition evaluation of later ECA nodes, event generation for cross-node or cross-strategy communication.

**Callback and Correlation.** For asynchronous actions, the system must be able to correlate external completion signals back to the correct graph instance, ECA Node, and action execution. Therefore, every asynchronous action should generate a correlation identifier when submitted. When a callback is received, the runtime validates the correlation identifier, checks whether the callback has already been processed, updates the action state, persists the result, and resumes the suspended execution flow if appropriate. This prevents duplicate callbacks, out-of-order callbacks, and unrelated external events from corrupting the graph execution state.



#### Failure Handling

Action failures should be handled according to explicit failure policies. Common policies include:

- **Retry**: The action is retried according to a configured retry strategy, such as fixed interval, exponential backoff, or maximum retry count.
- **Skip**: The action is skipped when failure is acceptable and does not block the ECA node.
- **Fail**: The current ECA node is marked as failed, preventing downstream ECAs from being executed.
- **Compensate**: A compensating action is triggered to undo or neutralize previous side effects.
- **Manual Intervention**: The execution is suspended and requires human review or operational handling.

## Relationship: ECA Graph

While a single ECA rule represents an isolated event response, complex business strategies often require multiple ECA rules to be composed. In such cases,  a approach to designing associations among ECA rules is to use a **directed acyclic graph (DAG)** to model the relationships between multiple ECA rules. Each ECA rule can be encapsulated as a node in the graph, making it the most fundamental execution unit—referred to as a **ECA Node**—within the system. The dependencies and execution order among these units are defined by the edges of the DAG, ensuring that all ECA rules are executed in topological order while also enabling scheduling opportunities for nodes that can run in parallel.

1. **Strategy (ECA Graph):** A directed acyclic graph composed of multiple ECA nodes and their dependency relationships. It defines the complete execution flow in complex scenarios. By orchestrating ECA nodes—such as sequencing, parallel execution, and conditional branching—it describes the system’s overall behavior and decision paths.

2. **ECA Node:** The basic node within a Strategy, encapsulating a complete ECA logical unit. It receives inputs, evaluates its internal Conditions, executes the specified Action when those conditions are met, and produces outputs. The dependency relationships between ECA Nodes determine the topological execution order and make the ECA Node the smallest building block of an executable workflow.

### Strategy Group

When a business scenario becomes too large to be represented by a single ECA Graph, the system can introduce a higher-level composition model and orchestration boundary called a Strategy Group. A Strategy Group is a container that organizes multiple Strategies and defines how they interact with each other. From the perspective of the Strategy Group, each Strategy is treated as a black-box execution unit with explicit inputs, outputs, trigger rules, and completion semantics.

![202602060036](./assets/202602060036.svg)

## Runtime Execution

### Definition phase and Runtime phase

An ECA rule or an ECA graph exists in two different phases: the **definition phase** and the **runtime phase**. (We'll use a ECA graph as an example, and the ECA rule works the same way.)

1. In the **definition phase**, the graph describes the static structure of the strategy and the rule used to generate the instance. At this stage, the graph is only a blueprint. It does not represent any specific execution and does not carry runtime state.
2. In the **runtime phase**, when a triggering event is received, the system instantiates the definition ECA graph into a concrete runtime instance. Each graph instance represents one logical execution of the strategy for a specific business context, such as a user, an order, a campaign, or a callback request. Since the same event may be delivered multiple times due to retries, network retransmission, repeated user operations, or duplicated callbacks, the runtime must be able to determine whether two trigger requests refer to the same logical graph execution.

![202602052353](./assets/202602052353.svg)

#### Instance idempotency key

The **Instance Idempotency Key** is the deterministic key used to identify one unique ECA graph instance. It is generated at runtime according to the key-generation rule defined in the definition ECA graph. The key is usually composed of stable attributes carried by the triggering event or derived from the execution context. The purpose of the instance idempotency key is to guarantee **graph-level idempotency**. For the same logical transition request, whether the system receives the trigger once or multiple times, it should create or resume exactly one graph instance and produce only one correct transition effect. This prevents duplicated state transitions, repeated reward issuance, duplicated points crediting, repeated message sending, or inconsistent graph execution state. 

The key should be designed according to the following principles:

1. **Deterministic**: The same logical trigger must always produce the same key.
2. **Business-stable**: The key should be based on stable business identifiers, such as user ID, order ID, campaign ID, task ID, callback ID, or transaction ID.
3. **Scoped**: The key should include the strategy or graph identity, such as `strategy_id` and `graph_version`, to avoid collisions between different strategies or graph definitions.
4. **Round-aware**: If the same business object is allowed to enter the same definition graph multiple times, the key should include a `round` or execution sequence number.
5. **Side-effect safe**: The graph-level key identifies the graph instance, but actions that produce external side effects should also define their own action-level idempotency keys.

#### Multiple Instantiations: Rounds

To support multiple instantiations and executions of a single definition ECA Graph in a instantiating idempotency key, we introduce a instantiating idempotency key dimension, **Rounds**, which identifies the specific execution round of the ECA graph within the instantiating idempotency key. In addition, the maximum number of execution rounds can be defined as a property of the ECA graph.

### Execution flow

1. **Triggering and Executable Frontier Selection**: When the system receives an event, it first retrieves all ECA nodes that are currently in the executable state. Then, based on the trigger conditions, it traverses these nodes to select the first executable node in each node path and aggregates them into a frontier node set. The core purpose of this step is to focus on the starting of each path, avoiding repeated processing of nodes within the same path, thereby ensuring process efficiency and logical clarity.
2. **Iterate over Frontier Nodes and Execute Calculation Logic**: The system processes each node in the frontier node set sequentially. For each frontier node, the rule engine is first invoked to execute the calculation logic for the node—this is the core computational step, determining the that the node should receive. Next, the system checks whether the node has been completed: if the node is not completed, subsequent processing is skipped, and the system moves directly to the next frontier node; if the node is completed, it proceeds to handle subsequent nodes, advancing the node status forward.
3. **Recursive Processing of Subsequent nodes (Core Logic)**: After the current frontier node is completed, the system retrieves all nodes associated as its subsequent nodes and evaluates each one. It first checks whether the subsequent node currently meets its start conditions; if it cannot start, it is temporarily skipped. If it can start, its status is updated to the executable state and the system immediately executes the full “node calculation logic” recursively for this node. This loop continues, forming a recursive processing mechanism that allows the node chain to automatically and coherently advance step by step until the path ends.
4. **Process Completion**: Once the last node in the frontier node set has been processed—that is, all starting nodes and their triggered subsequent recursive chains have completed calculation and status evaluation—the entire calculation process concludes. At this point, the system has completed all node computations and status updates driven by the triggering event for this round.

![202512310127](./assets/202512310127.svg)



#### Transitions between Nodes

In an ECA Graph, transitions define how the completion, failure, or invalidation of one ECA Node affects the execution eligibility of other nodes. A transition does not directly execute the target node. Instead, it determines whether the target node can move from a non-executable state, such as `Pending` or `Blocked`, into the `Ready` state. Once a node becomes `Ready`, it can be scheduled by the runtime and then enter the normal ECA lifecycle: condition evaluation, action execution, and result emission.

##### Vertical transitions: parent-to-child dependency

A vertical transition defines when a child node is allowed to start based on the execution results of its parent nodes. In a DAG, a child node may depend on one or more parent nodes. The transition policy determines how many parent nodes must reach a terminal state before the child node becomes eligible for execution. The most common vertical transition policies are:

- **All Completed (AND)**: The child node becomes Ready only after all of its parent nodes have reached the Completed state. This policy is suitable for strict dependency scenarios where every prerequisite must be satisfied before the next step can begin.
- **Any One Completed (OR)**: The child node becomes Ready as soon as any one of its parent nodes reaches the Completed state. This policy is suitable for alternative-path scenarios where multiple upstream branches can independently unlock the same downstream node. Once the child node has been activated, later completion events from other parent nodes should normally be treated as late signals and must not trigger duplicate execution unless the node is explicitly configured as re-entrant.
- **Custom Quantity (M-of-N)**: The child node becomes Ready when at least M out of N parent nodes have reached the Completed state. This policy is useful when a business process requires a minimum number of prerequisites to be satisfied, but does not require all of them. For example, a qualification node may start once any two out of three verification methods have passed.
- **Custom Predicate:** The child node becomes Ready when a user-defined transition predicate evaluates to true over the parent node results, graph context, and event attributes. This is useful for complex dependency logic that cannot be expressed by simple AND, OR, or M-of-N policies.

##### Branch-level Coordination Policy

Branch-level Coordination Policy defines how sibling nodes under the same parent or branch group interact with each other. Unlike vertical transitions, which determine whether a child node can start, branch-level coordination  determine how multiple candidate branches are coordinated once they become eligible. The most common policies are:

- **Mutual Exclusion**: Only one sibling branch may be selected. Once one sibling node is selected according to the branch selection rule, the remaining sibling nodes are marked as Invalid or Skipped and will no longer be scheduled in the current graph instance. The selection moment must be clearly defined, such as when a node first becomes Ready, when its condition evaluates to true, when it enters Running, or when it reaches Completed. In most business scenarios, mutual exclusion should be resolved at condition-match time or branch-selection time to avoid multiple branches producing conflicting side effects.
- **Parallel**: All sibling nodes are independent and may become Ready according to their own vertical transition rules. The execution of one sibling does not prevent the others from executing.
- **Priority Selection**: Sibling nodes are evaluated in a predefined priority order, and the first node whose condition is satisfied is selected for execution. Lower-priority siblings are invalidated or skipped. This policy is useful when multiple branches may be valid at the same time but the business requires deterministic selection.
- **Sequential Dependency**: Sibling nodes are logically ordered even though they share the same parent. A later sibling can start only after the previous sibling has completed. This policy is useful when the graph structure groups several related child nodes under the same parent for modeling convenience, but the runtime must still execute them in a deterministic sequence.

### Communication

In an ECA-based strategy execution model, communication defines how execution results, state changes, and contextual data are propagated across ECA Nodes and across Strategies.

#### Cross-Node Communication

Cross-node communication describes how one ECA Node influences another node within the same ECA Graph. There are three common communication mechanisms between ECA Nodes.

1. **Communication by event**:

2. **Communication to condition**: 

#### Cross-Strategy Communication

Cross-strategy communication describes how one Strategy interacts with another Strategy.



