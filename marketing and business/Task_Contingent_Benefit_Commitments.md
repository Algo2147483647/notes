# Task-Contingent Benefit Commitments

A **task-contingent benefit commitment** is an incentive mechanism in which a platform promises a benefit in exchange for the completion of specified user actions. Based on its business objectives, the platform defines the **commitment** by specifying the required **actions**, applicable rules, participation window, execution path, and promised **benefits**, and then presents it to eligible users.

Users may choose whether to **participate** by accepting the task. Once accepted, the system tracks their behavioral **progress** and evaluates whether the completion criteria have been satisfied. When the task is completed, the promised benefit is delivered subject to applicable budget and risk-control constraints. The user may then be offered another task or participation opportunity, forming a recurring incentive loop.

> **Configure commitment → Present commitment → User accepts → User acts → Track progress → Deliver benefit → Re-engage**

The mechanism converts desired platform behaviors into explicit, reward-backed tasks that users can voluntarily pursue. It is particularly useful for sustained behavioral guidance, such as encouraging repeated product usage or developing long-term usage habits.

From the user’s perspective, it reduces uncertainty by clearly communicating **what action is required, what benefit is available, and how far the user has progressed**. From the platform’s perspective, it enables benefits to be allocated conditionally against desired behaviors and fulfilled only when defined outcomes are achieved, improving both incentive efficiency and behavioral conversion.

## 1. Tasks

A **task** is the primary user-facing object in this mechanism. It represents a conditional commitment: if the user satisfies the defined completion criteria, the corresponding benefit becomes available. A complete incentive task typically defines three elements:

| Element                 | Description                                                  |
| ----------------------- | ------------------------------------------------------------ |
| **Required action**     | What the user is expected to do, such as placing an order, making a payment, checking in, browsing, sharing, or using a specific service. |
| **Completion criteria** | The conditions that determine successful completion, such as completing three orders, checking in for seven consecutive days, or browsing a page for at least ten seconds. |
| **Benefit**             | What the user receives upon completion, such as coupons, points, lottery chances, membership benefits, or eligibility for a subsequent task. |

In addition, the task may define **participation eligibility**, which determines who can enter the task based on criteria such as location, user segment, participation window, or business context.

### 1.1 Definition and Runtime

A task exists at two levels:

1. **Definition state**: The platform-configured task definition that specifies the task content, benefit, eligibility rules, and completion criteria. It serves as the blueprint for future participation.

2. **Runtime state**: The user-specific participation instance created when a user joins the task. It records the applicable task definition, participation time, current progress, completion status, and benefit fulfillment status.

This separation is important because a task definition may change over time or become unavailable to new participants, while existing participation instances may still need to follow the rules that applied when they were created. Therefore, the runtime instance should preserve or reference the applicable version of the task definition rather than implicitly adopting later changes.

### 1.2 Protection of Rules After Participation

Once a user joins a task, the applicable rules should generally be fixed for that participation instance. Subsequent progress calculation, completion evaluation, and benefit fulfillment should therefore follow the rules in effect at the time of participation.

To preserve this contract, the system should create a **task-rule snapshot** when participation is confirmed. At a minimum, the snapshot should capture the task objective, validity period, progress rules, benefit definition, fulfillment conditions, risk-control constraints, and any user-facing terms that materially affect the commitment.

Subsequent changes to the task definition must distinguish between two effects:

1. **Admission changes:** whether the task remains available to new participants.
2. **In-flight changes:** whether existing participation instances are affected in their progress calculation, completion criteria, or benefit fulfillment.

As a general principle, closing or modifying a task for future participants should not alter the commitment already made to existing participants. Their expected benefits should continue to be governed by the applicable snapshot unless the original terms explicitly allow otherwise or exceptional conditions—such as fraud, risk-control intervention, inventory exhaustion, or system failure—justify different handling.

### 1.3 Personalized Tasks

Tasks may be personalized based on user attributes or business context. The platform may vary task objectives, completion thresholds, benefits, or user-facing content according to factors such as location, user segment, historical behavior, membership tier, business scenario, or acquisition channel.

For example, users in different membership tiers may receive different completion thresholds for the same task template, such as a cumulative mileage requirement dynamically determined by membership level.

Once the personalized task is presented and the user confirms participation, the resolved task parameters should be fixed for that participation instance and preserved as part of its rule snapshot. Subsequent progress calculation, completion evaluation, and benefit fulfillment should follow the personalized rules accepted by the user at the time of participation.

## 2. Participation Strategies

Participation strategies determine which users may participate in a task, when they may participate, whether they may participate repeatedly, and how the platform intends to form incentives.

### 2.1 Participation Eligibility

Participation eligibility rules determine whether a user can obtain a participation opportunity for a given task. Common conditions include:

| Condition               | Examples                                                     |
| ----------------------- | ------------------------------------------------------------ |
| User conditions         | New users, existing users, inactive users, high-value users, or members. |
| Geographic conditions   | Specified cities, service areas, stores, or delivery zones.  |
| Time conditions         | During a campaign period, within a calendar day, within a calendar week, or during holidays. |
| Behavioral conditions   | Users who have not completed their first order, have not placed an order recently, or have browsed but not paid. |
| Frequency conditions    | Participation limited to once per user, once per week, or repeatable after completion. |
| Risk-control conditions | Exclusion of abnormal accounts, fraudulent behavior, bulk registrations, or high-risk transactions. |

The system uses these conditions to determine whether a task should be displayed to a user or whether a new participation opportunity should be generated for that user.

### 2.2 Timing of Participation

The timing of participation determines whether a task functions as an **ex ante incentive** or an **ex post reward**.

If the user sees the task, understands it, and confirms participation before the target behavior occurs, then the task may influence subsequent behavior and therefore constitutes an ex ante incentive.

If the user is included in the task only after completing the target behavior, or is informed after the fact that a reward is available, then the mechanism is closer to an ex post reward, compensation, or relationship-maintenance measure rather than a behavioral incentive in the strict sense.

The two types differ as follows:

| Type              | Temporal Sequence                                            | Primary Function                                             |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Ex ante incentive | User sees the task → User confirms participation → User performs the required action | Changes user decision-making and guides the user toward the target behavior. |
| Ex post reward    | User performs the behavior → Platform informs the user of the reward or issues a supplemental reward | Improves user satisfaction and strengthens positive feelings and future expectations toward the platform. |

Therefore, when designing participation timing, the platform must first clarify its objective: whether it seeks to change user decisions before the behavior occurs, or to improve user perception after the behavior has already occurred.

### 2.3 Modes of Participation

The **mode of participation** determines how a user enters a task and influences task reach, user awareness, participation friction, and behavioral attribution.

| Participation Mode                   | Advantages                                                   | Risks or Limitations                                         |
| ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Explicit opt-in                      | The user clearly perceives the task and actively commits to participating, making the incentive more salient and subsequent behavior easier to attribute. | Adds friction to the user journey and may cause drop-off before participation or task completion. |
| Automatic enrollment                 | Coverage is broad, and user effort is low.                   | Users may not sufficiently perceive the task, so the incentive effect may be limited. |
| Trigger-based invitation             | Users can be reached precisely in specific scenarios.        | The trigger timing must be accurately identified; otherwise, the optimal incentive window may be missed. |
| Default enrollment with confirmation | Combines broad exposure with an explicit participation step, balancing reach and user commitment. | Still requires clear communication and may introduce confirmation friction. |
| Post-behavior enrollment             | Minimizes interruption and may increase perceived acceptance of the benefit. | Functions more like an ex post reward than a true ex ante incentive because participation occurs after the target behavior. |

In practice, participation design should balance three objectives:

1. **Salience:** whether the user clearly understands the task and benefit before acting.
2. **Friction:** whether participation requires minimal additional effort.
3. **Attribution:** whether the platform can reasonably associate subsequent behavior with the incentive.

### 2.4 Repeat Participation

Repeat participation rules determine whether users may participate in the same type of task more than once. Common models include:

1. **One-time participation.** A user may participate only once, such as in a new-user first-order task.
2. **Periodic participation.** Participation opportunities reset according to a defined cycle, such as daily, weekly, monthly, or another configured period. Examples include daily check-in tasks or completing three orders within each calendar week.
3. **Progressive participation.** A new participation opportunity is unlocked only after the current round reaches the required state, typically completion. For example, a user may receive up to 12 rounds of a train-travel cashback task per year, with the next round becoming available no earlier than the following calendar day after the previous round is used.

Progressive participation is useful for creating a sustained behavioral journey. Its configuration should clearly define the maximum number of rounds, unlock conditions, waiting interval, and any progression in task requirements or benefits.

## 3. Task Objectives

A task objective specifically defines the behavior that the user needs to complete. It determines which behaviors may be counted toward the task, what level of performance constitutes completion, and what reward is triggered upon completion.

### 3.1 Components of a Task Objective

A task objective usually includes the following elements:

| Element                    | Description                                                  | Examples                                                     |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Behavior                   | The action the user needs to perform.                        | Place an order, pay, check in, browse, click, or share.      |
| Completion standard        | The quantity, amount, duration, or status required for completion. | Complete three orders, accumulate payments of at least 100 yuan, or check in for seven consecutive days. |
| Validity conditions        | Conditions used to determine whether a behavior can be counted. | Specified city, vehicle type, category, or channel.          |
| Time range                 | The time period within which the behavior must occur.        | Within 24 hours after participation, within the current week, or after 18:00 each day. |
| Spatial range              | The location or service area within which the behavior must occur. | Specified cities, stores, routes, service areas, or geofences. |
| Business rules             | Restrictions related to the specific business context.       | Specified payment method, order type, minimum transaction amount, or membership level. |
| Progress calculation rules | How the system accumulates, deduplicates, updates, or retrospectively adjusts progress. | Deduplicate by order ID, accumulate by day, or deduct progress after refund. |
| Reward linkage             | What reward or subsequent task is triggered after task completion. | Issue coupons, award points, grant lottery eligibility, or unlock the next stage. |
| User-facing explanation    | How the task requirements and current progress are displayed in the user interface. | “Complete one more order to receive a 10-yuan coupon.”       |

A task objective must be specific, executable, and computable. Users must be able to understand it, the system must be able to calculate it accurately, and customer service and operations teams must be able to explain it clearly.

### 3.2 Atomic Tasks and Composite Tasks

Task objectives may be simple or composite.

An **atomic task** is the smallest task unit, such as “complete one order,” “browse a page for ten seconds,” or “check in once.” Such tasks have a single objective and relatively simple calculation rules.

A **composite task** consists of multiple sub-objectives and is suitable for more complex operational scenarios. Common composition patterns include:

| Composition Pattern | Meaning                                                      |
| ------------------- | ------------------------------------------------------------ |
| Sequential          | The user must complete multiple steps in a specified order.  |
| Tiered              | The user obtains different reward tiers after reaching different levels of completion. |
| Parallel            | Multiple objectives can progress at the same time.           |
| Any-satisfied       | Completing any one sub-objective constitutes completion of the overall task. |
| All-satisfied       | All sub-objectives must be completed before the overall task is considered complete. |
| Repetitive          | The same objective can be completed repeatedly, with repetition here referring to recurring processes within a single participation task and thus reflecting a lower-level capacity for repetition. |
| Conditional routing | Users are assigned to the appropriate task pathway according to their previous completion status. |

Composite tasks are more flexible but also more likely to generate disputes over comprehension and calculation. Therefore, the user-facing presentation, progress calculation, and reward rules of composite tasks must remain consistent, so as to avoid discrepancies between the task logic displayed to users and the logic actually used by the system.

### 3.3 Fallback Rules for Non-User-Caused Failure

Some tasks depend on factors beyond the user’s control, such as merchant fulfillment, inventory availability, system stability, payment infrastructure, or service capacity. As a result, a user may perform the required action in good faith but still fail to satisfy the formal completion criteria.

For example, an order may be canceled by the merchant, a payment attempt may fail because of a platform outage, or a required service may be unavailable when the user arrives. When failure is attributable to such external factors rather than to the user, the task should not automatically be treated as unsuccessful.

The task mechanism should therefore define **fallback rules** for non-user-caused failures. Depending on the scenario, the system may grant equivalent progress, extend the validity period, fulfill the benefit directly, provide an alternative benefit, or escalate the case for manual review.

The objective is to ensure that risks outside the user’s control do not unfairly invalidate an otherwise legitimate participation and to preserve the credibility of the platform’s commitment.

## 4. Progress Calculation and Behavioral Attribution

Progress calculation is one of the most dispute-prone aspects of task-based incentive mechanisms. It must answer the following questions: Which user behaviors can be counted toward the task? How much do they count? Has the task been completed? If not, why not?

The system should not merely store a simple progress number. It should also store behavioral records and the basis for calculation. Only in this way can the platform explain task outcomes in user inquiries, dispute resolution, risk-control review, and financial reconciliation.

### 4.1 Information Required for Progress Calculation

Progress calculation should include at least the following information:

| Information         | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| Target progress     | How far the user remains from task completion.               |
| Included records    | Which orders, behaviors, or events have been counted toward progress. |
| Excluded records    | Which behaviors have not been counted, and why.              |
| Time window         | Which behaviors occurred within the valid time range.        |
| Deduplication rules | Whether the same order or event can be counted only once.    |
| Node attribution    | Which task node a behavior belongs to, so as to avoid duplicate counting. |

For example, suppose a user participates in a task that promises a coupon after completing three orders in the current week. The system should not only display “2/3 orders completed,” but should also be able to explain which two orders were counted and which order was excluded because of refund, timeout, city mismatch, or ineligible order type.

### 4.2 Basic Logic of Progress Calculation

Progress calculation generally involves four steps:

1. Record actual user behaviors, such as browsing, clicking, placing an order, paying, refunding, or canceling.
2. Filter valid behaviors according to the task rules, such as whether the time, city, order type, amount, and payment status meet the requirements.
3. Calculate progress according to the task rules, such as counting, accumulating amounts, determining continuity, or verifying whether steps were completed in sequence.
4. Generate an explainable progress result, including included behaviors, excluded behaviors, and the final completion status.

Behavioral records should remain as factual as possible and should not be prematurely bound to a specific task. The same order or behavior may be relevant to multiple tasks, multiple rewards, or multiple risk-control rules at the same time. The system should first preserve the factual record and then calculate outcomes according to different task rules.

### 4.3 Common Types of Progress

| Progress Type            | Examples                                                     |
| ------------------------ | ------------------------------------------------------------ |
| Count-based progress     | Complete three orders; browse a page five times.             |
| Amount-based progress    | Accumulated payment amount reaches 100 yuan.                 |
| Tiered progress          | Obtain different rewards after completing one, three, or five orders. |
| Boolean progress         | Whether one browsing action or one check-in has been completed. |
| Path-based progress      | Browse first, then place an order, then complete payment.    |
| Composite progress       | Complete two orders and reach a cumulative amount of 80 yuan. |
| Exclusion-based progress | Count only orders that did not use a specified coupon.       |

For complex tasks, progress calculation should place special emphasis on explainability. What users see is task progress; what the system calculates is a rule-based result. The two must be traceable to each other.

## 5. Reward Mechanism

A reward is the benefit that the platform grants and actually delivers after the user completes a task. The reward process is not simply “issue immediately after task completion.” It usually involves three stages: reward commitment, eligibility confirmation, and reward fulfillment.

### 5.1 Three Layers of Rewards

| Layer              | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| Reward commitment  | The reward content displayed by the platform before participation, such as “complete three orders to receive a 20-yuan coupon.” |
| Reward eligibility | The system determines whether the user satisfies the conditions for receiving the reward after completing the task. |
| Reward fulfillment | The platform actually issues the reward, such as coupons, points, red packets, or unlocked benefits. |

These three layers must be distinguished. User completion of a task does not necessarily mean that the reward has already been received. The platform may still need to verify inventory, budget, risk-control status, and fulfillment feasibility. However, if these restrictions may affect the user’s ultimate ability to claim the reward, the platform should disclose them in the task rules in advance and should not impose new restrictions only after the user has completed the task.

### 5.2 Pre-Issuance Verification

Before issuing a reward, the system usually needs to verify the following:

| Verification Item                   | Examples                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| Whether the task has been completed | Whether the user behavior has reached the task objective.    |
| Whether the reward remains issuable | Whether the budget, inventory, coupon package, or benefit asset is available. |
| Whether the user presents risk      | Whether there is fraud, order brushing, abnormal trading, bulk registration, or other risk behavior. |
| Whether the order status is stable  | Whether there is a refund, cancellation, dispute, or payment failure. |
| Whether issuance succeeds           | Whether the benefit system, coupon system, points system, or account system successfully issues the reward. |

Risk control is not an external add-on to the reward process; it runs through the entire task lifecycle. Before task display, risk control may determine whether a user is eligible to see or join the task. After task completion, it may determine whether the user has obtained reward eligibility. Before reward issuance, it may conduct a final check to prevent abnormal reward outflows. However, risk-control rules also need to remain clear and explainable. For normal users, the platform should avoid denying rewards through vague statements such as “the system has determined that the conditions were not met,” because such explanations undermine user trust.

## 6. Business Challenges

Task-based incentives can improve short-term conversion and engagement, but persistent or poorly designed incentives may create long-term behavioral and relationship costs. Two common challenges are **incentive dependence** and **near-completion failure**.

### 6.1 Incentive Dependence

Long-term task incentives may cause users to become dependent on reward conditions. When users repeatedly see messages such as “complete the task to receive a reward,” they may gradually form an expectation that certain behaviors, which might otherwise have occurred naturally, should also be subsidized by the platform. Over time, users may stop placing orders, visiting pages, or using services based on genuine demand. Instead, they may first check whether a task is available, whether the reward is sufficient, and whether the subsidy is worthwhile. This is incentive dependence: user behavior gradually shifts from demand-driven to reward-driven.

Therefore, the platform should not focus only on the conversion rate of individual tasks, but should also consider long-term effects. Task design should gradually shift from subsidy-driven acquisition to habit formation. In the early stage, stronger rewards may be used to reduce the cost of user trial. In the middle stage, continuous tasks may reinforce usage paths. In the later stage, subsidy intensity should be gradually reduced, so that users continue to stay and use the service more because of service value and usage habits.

### 6.2 Near-Completion Failure

Task mechanisms can easily produce the negative experience of “almost completing” a task. For example, a user sees the prompt “complete one more order to receive a 20-yuan reward,” but ultimately fails to obtain the reward because of timeout, order cancellation, system delay, or misunderstanding of the rules. In such cases, the user’s negative reaction is often much stronger than it would be for an ordinary unclaimed discount.

The reason is that the user has already incurred behavioral costs and is very close to the target. Psychologically, the reward has become highly concrete and may even be perceived as a benefit that has almost already been obtained. Once the task fails, the user may not simply believe that they failed to complete the task; instead, they may believe that the platform’s rules were unclear, that the calculation was unfair, or even that the platform failed to honor its commitment. Therefore, the platform must pay particular attention to relationship repair after near-completion failures. Possible measures include:

1. Clearly displaying remaining progress and deadlines during the task;
2. Sending advance reminders to users who are likely to fail soon;
3. Providing compensation or manual review for failures caused by non-user factors;
4. Providing clear reasons for non-completion in rule-intensive tasks;
5. Offering fallback benefits for high-value users or highly disputed scenarios.

Handling task failure is not merely a customer-service issue, nor is it simply a matter of reward cost. It concerns whether users continue to trust the platform’s task rules, whether they remain willing to participate in future incentive programs, and whether they perceive the platform as fair and credible.

