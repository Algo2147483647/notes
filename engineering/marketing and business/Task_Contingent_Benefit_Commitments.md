# Task-Contingent Benefit Commitments

A **task-contingent benefit commitment** is an operational mechanism through which a platform motivates users to complete specified actions by promising rewards upon task completion. Based on its operational objectives, the platform configures conditional benefit ***commitments*** and informs users that, within a defined time window, through a specified path, and under stated rules, they may obtain certain ***benefits*** by completing designated ***actions***. After seeing the commitment, users may decide whether to ***participate***. Once they accept the task, the system continuously records their behavioral ***progress*** and determines, according to the applicable rules, whether the target has been achieved. Upon completion, the platform delivers the promised benefit subject to budgetary and risk-control constraints, and may further guide the user into a new round of tasks or another participation opportunity, thereby forming a closed loop of sustained incentives.

> **Configure the commitment → Display the commitment → User accepts → User performs the required action → Progress is measured → Benefit is delivered → User participates again**

This system transforms “the behavior the platform wants users to perform” into “a task users are willing to actively complete in order to obtain benefits.” It is commonly used for long-term behavioral guidance, especially for cultivating user mindsets and usage habits. From the user’s perspective, the system reduces uncertainty by making clear what needs to be done, what can be obtained, and how much progress has been made. From the platform’s perspective, subsidies shift from indiscriminate distribution to targeted configuration around desired behaviors and performance-based fulfillment, thereby improving benefit allocation efficiency and user action conversion.

## 1. Tasks

A task is the core object that users can directly see and understand in this mechanism. It represents a conditional commitment: once the user completes a specified action, the user may obtain a corresponding reward. A complete incentive task usually needs to specify three types of information:

| Information                            | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ |
| What the user needs to do              | For example, place an order, make a payment, check in, browse, share, or use a specific service. |
| What counts as completion              | For example, complete three orders, check in for seven consecutive days, or browse a page for at least ten seconds. |
| What the user receives upon completion | For example, coupons, points, lottery chances, membership benefits, or eligibility for the next-stage task. |

The platform must also define whether a user is eligible to participate in the task, such as whether the user belongs to a specified city, user segment, time window, or business scenario.

### 1.1 Rule Definition and User Participation Records

A task can be understood at two levels.

1. **Definition state**, namely the task rules configured by the platform. This level serves operational objectives and specifies the task content, reward content, participation conditions, and completion criteria.

2. **Runtime state**, namely the participation record generated after a user joins the task. This level is user-specific and records which task the user participated in, when the user joined, which rules applied at that time, what the current progress is, and whether the user ultimately completed the task and received the reward.

This distinction is crucial. The platform may later modify how a task is displayed or may stop making the task available to new users. However, this does not necessarily mean that users who have already joined the task should automatically be subject to the updated rules.

### 1.2 Protection of Rules After User Participation

Once a user confirms participation in a task, the platform should preserve the task rules applicable at the time of participation. In principle, subsequent progress calculation, task completion judgment, and reward issuance for that user should all be based on those rules. Therefore, the system should generate and store a task-rule snapshot when the user confirms participation. At a minimum, the snapshot should include the task objective, validity period, progress calculation rules, reward content, reward issuance conditions, risk-control restrictions, and necessary user-facing copy.

If the platform later modifies the task rules, suspends task display, or stops allowing new users to participate, the system must clearly distinguish between two situations:

1. Whether the task is merely closed to new participants;
2. Whether the change affects the progress calculation and reward issuance of users who have already joined.

In general, users who have already participated should not have their expected benefits arbitrarily reduced because of subsequent rule changes by the platform. Unless the task rules have explicitly stated this possibility in advance, or unless special circumstances exist, such as fraud, risk events, inventory exhaustion, or system abnormalities, the platform should continue to fulfill the commitment according to the rules in effect when the user joined.

### 1.3 Personalized Tasks

Tasks may also be generated on a personalized basis. The platform may configure different task objectives, reward content, or display copy for different users according to their city, user segment, historical behavior, business scenario, or acquisition channel. For example, when users at different membership tiers participate in the same task, the target thresholds they are required to meet may vary by tier; for instance, the required cumulative mileage can be dynamically adjusted according to membership level.

Once a personalized task is displayed to a user and the user confirms participation, it should become part of that user’s participation record. Thereafter, the system should calculate progress and issue rewards according to the personalized rules that the user accepted at that time.

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

Different modes of participation affect task reach, user perception, and subsequent behavioral attribution.

| Participation Mode                         | Advantages                                                   | Risks or Limitations                                         |
| ------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| User actively confirms participation       | The user’s perception is clear, willingness to participate is stronger, and a sense of commitment is easier to form. | The user journey is longer, and users may drop off during exposure, comprehension, clicking, confirmation, or action. |
| Automatic enrollment                       | Coverage is broad, and user effort is low.                   | Users may not sufficiently perceive the task, so the incentive effect may be limited. |
| Trigger-based invitation                   | Users can be reached precisely in specific scenarios.        | The trigger timing must be accurately identified; otherwise, the optimal incentive window may be missed. |
| Post-behavior enrollment                   | User interruption is relatively low, and acceptance may be higher. | Users are more likely to understand it as an ex post benefit rather than an ex ante incentive. |
| Default display with required confirmation | Balances task salience with user commitment.                 | Users still need to understand the value of the task, so page-level communication must be sufficiently clear. |

Task-based incentive mechanisms usually need to balance three objectives:

1. Whether the user can clearly perceive the task and reward before acting;
2. Whether the operational cost of participating is sufficiently low;
3. Whether the platform can reasonably determine whether subsequent behavior was attributable to the task.

### 2.4 Repeat Participation

Repeat participation rules determine whether users may participate in the same type of task again. Common models include:

1. **One-time participation.** Each user may participate only once, as in a new-user first-order task.
2. **Periodic participation.** The system refreshes the task by calendar day, week, month, or a customized cycle, such as daily check-in or completing three orders per week.
3. **Progressive participation.** The user must complete the current task before proceeding to the next round. For example, the platform may allocate each user 12 annual entries into the train-travel cashback program. After one entry has been used, the next entry becomes available on the following calendar day.

Progressive participation is suitable for constructing a continuous behavioral path, but the rules for generating subsequent tasks must be clear. These include participation limits, unlocking conditions, waiting intervals, and the logic of reward escalation.

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

### 3.3 Fallback Rules for Task Failure Caused by Non-User Factors

Some tasks do not depend entirely on user behavior. Even if users have attempted to complete the task according to the rules, final task completion may still be affected by platform supply, merchant fulfillment, inventory, system stability, payment infrastructure, or delivery capacity. For example, the user may have placed an order but the merchant cancels it; the user may have attempted payment but encounters a platform system failure; or the user may have arrived at a specified location but the service is unavailable. In such cases, if task failure is not caused by the user, the platform should not simply deny the user’s entitlement.

Accordingly, the task mechanism needs fallback rules. For failures caused by the platform, merchants, systems, or fulfillment capacity, the platform may, depending on the circumstances, compensate progress, extend the task period, issue the reward retroactively, provide an alternative reward, or initiate manual review. The purpose is to prevent platform-side risks from being fully shifted to users and to preserve the credibility of the task commitment.

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

Task-based incentive mechanisms can improve short-term conversion and user activity. However, if used improperly over the long term, they may also create incentive dependence, distort user expectations, and increase the cost of relationship repair.

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

