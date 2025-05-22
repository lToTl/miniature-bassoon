## O. Core Concept: Software Testing - Ensuring Quality & Finding Defects

Software testing is a crucial, often complex, and economically significant discipline focused on confirming quality and finding problems (defects/bugs) in software systems. It aims to ensure software meets both explicit/implicit requirements and user expectations.

1.  **What is Software Quality?**
    *   **Definition**: The degree of conformance to explicit or implicit requirements and expectations.
    *   **Types**:
        *   **Functional Quality**: Does the system do what it's supposed to do? (*e.g., a pen writes*).
        *   **Non-Functional Quality**: How well does it do it? (*e.g., usability, performance, robustness, security, safety, maintainability, reliability*). These are often overlooked but critical (*e.g., Heartbleed vulnerability, Cruise car AI misinterpretation*).

2.  **Types of Quality Activities:**
    *   **Quality Assurance (QA)**: Managerial, process-oriented activities to prevent defects and ensure quality processes are followed (*e.g., defining development processes, training, auditing*).
    *   **Quality Control (QC)**: Technical, hands-on activities to identify defects after they've been introduced (*e.g., testing, reviews*).
    *   **Dynamic Testing**: Executing the system with inputs to observe behavior (*e.g., unit, integration, system testing*).
    *   **Static Testing**: Analyzing the system without executing it (*e.g., code reviews, static code analysis tools*).

3.  **Validation vs. Verification:**
    *   **Validation** ("Are we building the *right* system?"): Checking if the software meets user needs and expectations (user-focused, often at acceptance testing phase).
    *   **Verification** ("Are we building the system *right*?"): Checking if the software conforms to specifications and processes at each development stage (developer-focused, throughout the lifecycle).

4.  **Key Testing Terminology:**
    *   **Test Case**: A set of inputs, execution conditions, and an expected output. A test without an expected output is not a complete test case.
    *   **Test Data**: The input values provided to the system under test.
    *   **Test Oracle**: The mechanism or source that determines the correct expected output for a given test case.
    *   **Test Verdict**: The result of a test case (Pass/Fail) based on comparing the actual output to the expected output.
    *   **Test Suite**: A collection of test cases.
    *   **Test Script**: Automated instructions for executing a test case or sequence of test cases (*e.g., using frameworks like `JUnit`*).

5.  **The Bug Triad: Error, Fault, and Failure:**
    *   **Fault** (_or Defect/Bug_): An incorrect step, process, or data definition in a program's code or design. This is the "root cause" within the system itself (*e.g., `i=1` instead of `i=0` in a loop counter*).
    *   **Error**: An incorrect program state caused by a fault during execution (*e.g., a variable holding a wrong value, or program flow deviating from intended path*). A fault doesn't always lead to an error.
    *   **Failure**: The observable incorrect behavior of the system, perceived by the user, resulting from an error state being propagated (*e.g., wrong output displayed, system crash, security breach*). An error doesn't always lead to a failure (*e.g., a faulty line might not be executed, or its effect is masked*).

    Relationship: A **Fault** in the code, when executed with specific **Test Data**, can lead to an **Error** (incorrect state), which then may manifest as a **Failure** (incorrect external behavior). Testing primarily detects Failures, which then lead to Debugging to find the underlying Fault.

6.  **Challenges in Software Testing:**
    *   **Impossibility of Exhaustive Testing**: It's practically impossible to test all possible inputs and input combinations due to combinatorial explosion.
    *   **Smart Test Selection**: The "art of testing" lies in intelligently selecting a limited set of tests that are most likely to expose faults.
    *   **Metamorphic Testing**: A technique for testing systems where the expected output is unknown (*e.g., AI/ML systems, scientific computations*). It relies on "metamorphic relations" – properties describing how outputs should change (or not change) when inputs are transformed in a specific way (*e.g., for a mapping app, the distance from A to B should be the same as B to A*).

7.  **Economic Importance:**
    *   A significant portion of IT budget and development time (often 25-50%) is dedicated to testing and debugging. This highlights its critical role in delivering reliable and safe software.

---
---

## I. Software Testing: Debugging & Black Box vs. White Box Approaches

This lecture introduces debugging as the process of fixing identified problems and differentiates between black box and white box testing strategies for finding those problems.

1.  **Debugging: From Failure to Fault Correction**
    *   **Definition**: Debugging is the systematic process of identifying and correcting faults (bugs/defects) in software that have led to observed failures (incorrect system behavior). It's a developer activity, initiated after testing detects a failure.
    *   **Debugging Workflow**:
        *   **Failure Detection**: Testers (or users) observe unexpected or incorrect system behavior.
        *   **Issue Reporting**: A critical step. A good issue report is essential for efficient debugging.
            *   Key Components: Short summary, detailed description (inputs, expected vs. actual outputs, execution sequence, system state, software version, logs, screenshots), and most importantly, clear, reproducible steps for the developer to trigger the failure.
        *   **Fault Localization**: Developers use debugging tools to pinpoint the exact line(s) of code causing the failure.
        *   **Fixing**: Modifying the faulty code.
        *   **Regression Testing**: Rerunning existing tests to ensure the fix works and doesn't introduce new bugs.
    *   **Debugger Tools** (_e.g., IntelliJ Debugger_):
        *   Allow inspection of the program's state (variable values) at any point during execution.
        *   **Breakpoints**: Pause program execution at specified lines to examine variables.
        *   **Stepping**: Execute code line-by-line (step over, step into, step out) to trace execution flow and variable changes.

2.  **Homework 1: Hands-on Debugging**
    *   You will debug two Java programs, identifying faults based on provided issue reports.
    *   System 1: Heap Sort (Heapify Function): Debug a program that implements the heapification part of the Heap Sort algorithm.
    *   System 2: Eight Queens Problem (Genetic Algorithm):
        *   Eight Queens Problem: Place 8 non-attacking queens on an 8x8 chessboard.
        *   Genetic Algorithm (GA) Basics: An optimization algorithm inspired by natural selection.
            *   Starts with a population of random potential solutions.
            *   Evaluates solutions using a fitness function (*e.g., number of attacking queens; goal is a fitness of 0*).
            *   Iteratively generates new "generations" by selecting and combining "fitter" solutions from the previous generation (using operations like crossover and mutation).
        *   Debugging Challenge: This program is non-deterministic. Debugging requires understanding its probabilistic nature and how issues like slow convergence or incorrect fitness calculation can manifest as failures.
    *   **Task**: Document your debugging process: why you set specific breakpoints and how your reasoning evolved as you identified the fault. Propose and explain the code fix.

3.  **Black Box Testing vs. White Box Testing**
    These are two fundamental and complementary approaches to designing test cases.
    *   **Black Box Testing** (_Functional / Behavioral Testing_):
        *   Perspective: Views the software as an opaque "black box" without knowledge of its internal code or structure.
        *   Focus: Deriving test cases solely from the software's specification, requirements, and external behavior.
        *   Goal: Verify if the system meets its functional and non-functional requirements from a user's perspective.
        *   Techniques:
            *   **Equivalence Class Partitioning**: Dividing the input (and output) domain into sets (equivalence classes) where all values are expected to behave similarly. Test cases are selected to represent each class.
            *   **Boundary Value Analysis**: Testing values at the extreme ends or "boundaries" of equivalence classes, as these are common sources of errors.
        *   Pros: Tests against user needs; independent of implementation details; can be done by non-developers.
        *   Cons: Cannot guarantee full code coverage; may miss hidden faults (*e.g., dead code, malicious logic, or obscure error conditions not triggered by typical inputs defined by the spec*).
    *   **White Box Testing** (_Structural / Clear Box Testing_):
        *   Perspective: Requires knowledge of the software's internal code structure, algorithms, and implementation.
        *   Focus: Designing test cases to exercise specific code paths, branches, and statements.
        *   Goal: Verify the internal logic of the code; identify internal faults, dead code, or unhandled conditions.
        *   Techniques: Code coverage (statement, branch, path coverage), code reviews, symbolic execution.
        *   Pros: Ensures thorough internal logic verification; can pinpoint specific fault locations.
        *   Cons: Cannot detect missing functionality (requirements not implemented); may not identify discrepancies between the specification and the implemented behavior if the code logically reflects a flawed understanding of requirements.
    *   **Complementary Nature**:
        *   Both approaches are crucial for comprehensive testing.
        *   Black Box ensures the system meets user expectations and requirements.
        *   White Box ensures the implementation is robust and free of internal errors.
        *   Typically, developers perform white box testing (*e.g., unit tests*), while higher-level testing (system, acceptance) and end-user interactions are effectively black box.

---
---

## II. Black Box Testing: Specification-Based Test Design

This lecture focuses on Black Box Testing, a fundamental approach to designing test cases based purely on the system's external behavior and specification, without knowledge of its internal implementation.

1.  **Black Box vs. White Box Testing (Recap)**
    *   **Black Box Testing** (_Specification-based / Functional Testing_):
        *   Focus: What the system is supposed to do (based on requirements/specifications).
        *   Information Source: External specifications, user stories, requirements documents.
        *   Goal: Verify if the system meets its defined functions and non-functional requirements (*e.g., performance, security*).
        *   Limitation: Cannot detect unspecified functionality (*e.g., dead code, hidden malicious logic*) or internal structural problems not exposed by requirements.
    *   **White Box Testing** (_Structural / Implementation-based Testing_):
        *   Focus: How the system is implemented (based on source code, design).
        *   Information Source: Source code, architecture diagrams.
        *   Goal: Verify internal logic, ensure code coverage, identify faults in implementation.
        *   Limitation: Cannot detect missing functionality (requirements not implemented).
    *   **Complementary Nature**: Both are essential. Black Box validates the system against user needs; White Box verifies the internal correctness of the implementation.

2.  **Equivalence Class Partitioning (ECP)**
    *   Purpose: A systematic technique to reduce the vast input space into manageable, representative subsets for testing.
    *   Concept: Divide the input data space (and sometimes output data space) into equivalence classes (ECs). All values within an EC are expected to cause the same behavior from the software.
    *   **Key Rules/Properties**:
        *   Defined per variable: ECs are identified for each individual input and output variable, not for combinations of variables.
        *   No Overlap: Equivalence classes for a single variable must be mutually exclusive.
        *   Full Coverage: All possible inputs (valid and invalid) must be covered by at least one EC.
        *   Design Task: There's no single, unique way to partition. It requires interpretation of the specification and domain knowledge.
    *   **Process**:
        *   Identify all input variables (*e.g., age, X, Y, gender, side_a, side_b, side_c*).
        *   Identify all output variables (*e.g., isAdult, sum, errorMessage, perimeter, area, triangleType*).
        *   For each variable, define its ECs, including:
            *   Valid ECs: Ranges or specific values expected to produce correct, desired behavior.
            *   Invalid ECs: Values that are outside the expected valid range or type (*e.g., negative numbers for age, non-integers, "empty" inputs, "out of bounds" results for calculations*).
        *   Clarify Ambiguities: If the specification is vague (*e.g., exact age threshold, handling of invalid inputs*), consult the author/developer to establish clear expected behavior.
    *   **Test Case Generation from ECP**:
        *   Goal: Create a minimum set of test cases that ensures at least one value from every defined equivalence class is used as input and/or observed as output.
        *   Strategy for Multiple Inputs:
            *   Combine valid inputs from different ECs as much as possible to minimize tests.
            *   For invalid inputs: Each test case should ideally have only one invalid input value for a given variable, while other input variables are set to valid values. This helps isolate the fault's cause.

3.  **Boundary Value Analysis (BVA)**
    *   Purpose: To find errors that often occur at the "edges" of valid input ranges.
    *   Concept: An extension of ECP. Once ECs are defined, BVA focuses on values at and around the boundaries of those classes.
    *   Test Data Selection: For each boundary, include test cases for:
        *   The boundary value itself (*e.g., 18*).
        *   A value just inside the boundary (*e.g., 17, 19*).
        *   A value just outside the boundary (*e.g., 17, 81 for an 18-80 range*).

4.  **Combinatorial Testing (Brief Preview)**
    *   While ECP ensures each EC is covered at least once, it doesn't cover all combinations of ECs across multiple variables.
    *   Combinatorial testing aims to cover combinations (*e.g., pairwise, N-wise combinations*) of input values, which can be significantly more test cases than basic ECP but still far less than exhaustive testing. (Topic for next lecture).

5.  **Homework 2: Triangle Classifier**
    *   Task: Apply ECP and BVA to a triangle classification program (input: 3 side lengths; output: perimeter, area, triangle type, invalid/error message).
    *   **Crucial Warning**: Adhere strictly to the per-variable definition of equivalence classes as taught in the lecture. Do NOT define ECs based on combinations of input variables (*e.g., "sides that form an equilateral triangle"* as one EC). This is a common mistake and not how ECP is defined in this course.

---
---

## III. Software Testing: Advanced Black Box Techniques - Combinatorial Testing

This lecture extends Black Box Testing, moving beyond simple equivalence class partitioning to address the complexity of testing interactions between multiple input variables.

1.  **Beyond Basic Equivalence Class Partitioning (ECP)**
    *   Recap: ECP: Defines mutually exclusive, exhaustive subsets of input/output data per variable. Aims to cover each EC at least once with a minimum number of tests.
    *   Limitation of Basic ECP: While effective for covering individual variable behaviors, it does not explicitly test combinations of input values across different variables. Many bugs arise from unexpected interactions between inputs.

2.  **Cause-Effect Graphing (CEG)**
    *   Purpose: To systematically design test cases that expose failures caused by logical combinations of input conditions (causes) leading to specific outcomes (effects). It's a bridge between ECP and combinatorial testing.
    *   Process:
        *   Analyze the specification to identify all causes (input conditions, derived from ECs) and effects (outputs/behaviors).
        *   Define logical relationships (rules/business logic) between causes and effects (*e.g., "IF age is 18-80 AND gender is Male THEN accept policy"*).
        *   Represent these relationships graphically (cause-effect graph) or in decision tables.
    *   Benefit: Leads to a stronger test suite than basic ECP by explicitly testing critical interactions defined by the system's logic.
    *   Distinction from ECP (for Homework): CEG focuses on logical relationships/combinations of variables, whereas ECP strictly partitions each variable individually. Do not use CEG approach for the ECP homework.

3.  **Combinatorial Testing**
    *   Purpose: To efficiently test a large number of input combinations when exhaustive testing is infeasible. It focuses on finding a smaller, representative set of tests that maximize interaction coverage.
    *   Core Idea: Bugs are often triggered by interactions between a small number of variables. Combinatorial testing aims to cover all combinations up to a certain "strength" (T-way interaction).
    *   **T-way Interaction Testing**:
        *   Definition: Aims to cover all possible combinations of values (from their respective ECs) for any 'T' variables at a time, for all possible groups of 'T' variables.
        *   `T = 1` (One-Way): Equivalent to simple ECP (each EC covered once). Very weak for finding interaction bugs.
        *   `T = N` (N-Way, where N is total variables): Exhaustive testing. Impractical due to combinatorial explosion (*e.g., 34 boolean switches = 2^34 combinations*).
        *   Empirical Evidence (NIST Study): Studies show that even low-order T-way interactions (*e.g., 2-way, 3-way, 4-way*) can find a surprisingly high percentage of defects (*e.g., 90% of bugs found with 3-way interaction for many systems*), dramatically reducing the number of tests compared to exhaustive testing.
    *   The "Sweet Spot": Usually, `T=2`, `T=3`, or `T=4` offers a good balance between test effort and bug detection effectiveness.
    *   Calculating Combinations (Basic Example):
        *   If you have N variables, each with L possible values/ECs:
            *   Number of 1-way interactions: N * L (but often covered by L tests if L=2 and values can be packed).
            *   Number of pairs (for 2-way): N choose 2 (N * (N-1) / 2).
            *   Number of combinations for a single pair of variables (if each has L levels): `L * L = L^2`.
            *   The actual number of tests needed for T-way coverage is a complex optimization problem.
    *   Challenge: Manually creating a minimum set of T-way interaction tests (a "covering array") is extremely difficult for real-world problems.
    *   Solution: Automated Tools (_e.g., ACTS_):
        *   Specialized tools that generate covering arrays.
        *   Inputs to Tool:
            *   List of variables.
            *   Number of equivalence classes/levels for each variable.
            *   Desired interaction "strength" (T-value).
            *   (Optional) Optimization algorithm choice.
        *   Output: A compact set of test inputs (the covering array) that satisfies the specified T-way coverage.

4.  **The Test Oracle Problem in Combinatorial Testing**
    *   Limitation: Combinatorial testing tools (like `ACTS`) primarily generate input combinations.
    *   Missing Piece: They do not automatically generate the expected output for each of these combinations.
    *   Implication: While the tool efficiently tells you what to test, it doesn't tell you what the correct result should be. This is crucial for verifying correctness beyond simple "crash testing."
    *   Addressing the Problem:
        *   Manual inspection of outputs.
        *   Developing "plausibility checks" or "filters" based on known rules to flag obviously incorrect or impossible outputs.
        *   Relying on formal specifications (advanced approach).

5.  **Homework 2: Booking App**
    *   Task: Use the `ACTS` tool to generate covering arrays for a booking application.
    *   Steps:
        1.  Model the booking app's inputs as variables with their respective equivalence classes/levels.
        2.  Use `ACTS` to generate covering arrays with different interaction strengths (T-values).
        3.  Analyze the generated test inputs and the program's output.
        4.  Identify and analyze failures/crashes: are they distinct types of failures?
        5.  Address the test oracle problem: How will you determine if non-crashing outputs are correct or incorrect? (*e.g., identify rules for "impossible" output values*).

---
---

## IV. Software Testing: White Box Principles & Code Coverage Criteria

This lecture introduces White Box Testing, a method of testing that leverages knowledge of the software's internal structure and code, and details various code coverage criteria used to measure test adequacy.

1.  **White Box Testing Fundamentals**
    *   Definition: Also known as Clear Box, Open Box, Glass Box, Transparent Box, Code-Based, or Structural Testing. It involves designing test cases based on insights into the software's internal code, structure, and algorithms.
    *   Focus: Verifying the correctness of control flow, data flow, and algorithmic logic within the program.
    *   Contrast with Black Box: White box uses internal code knowledge to design tests, while black box uses external specifications.
    *   **Test Adequacy Criterion**: A measure used to define the effectiveness of a test suite by quantifying how much of the defined structural elements (*e.g., statements, branches*) in the program have been executed by the tests. Measured as (Covered Items / Total Items) * 100%.

2.  **Control Flow & Coverage Criteria**
    The core of white box testing is analyzing the program's control flow graph (CFG), which represents the execution paths through the code.
    *   **Control Flow Graph (CFG)**: A graphical representation of all possible execution paths within a program.
        *   Nodes: Represent individual statements or decision points.
        *   Edges (Branches): Represent the flow of control between nodes.
        *   Must have a single start node and a single end node.
    *   **Key Coverage Criteria** (from weakest to strongest practical):
        *   **Statement Coverage** (_Node Coverage_):
            *   Goal: Execute every executable statement (node in CFG) in the program at least once.
            *   Limitations: 100% statement coverage does not guarantee that all logical paths or conditions are tested, nor does it guarantee the absence of faults. It's a very weak criterion.
        *   **Branch Coverage** (_Decision Coverage_):
            *   Goal: Execute every possible outcome (true/false) of every decision point (*e.g., `if`, `while`, `for` conditions*) in the program at least once.
            *   Strength: Stronger than statement coverage; 100% branch coverage implies 100% statement coverage.
        *   **Condition Coverage**:
            *   Goal: Evaluate every individual boolean condition within a complex predicate (decision point) to both true and false at least once.
            *   Limitations: Does not necessarily imply 100% branch/decision coverage (*e.g., due to short-circuiting where not all conditions are evaluated*).
        *   **Condition Decision Coverage (CDC)**:
            *   Goal: Achieve 100% Branch/Decision Coverage AND 100% Condition Coverage.
        *   **Modified Condition/Decision Coverage (MCDC)**:
            *   Goal: A very strong criterion. For every condition in a decision, every possible outcome of that condition must be shown to independently affect the decision's outcome, while other conditions are kept constant.
            *   Importance: Often mandated for safety-critical systems (*e.g., aerospace software, DO-178C standard*).
            *   Strength: Implies 100% Decision Coverage and 100% Statement Coverage.
        *   **Multiple Condition Coverage (MCC)**:
            *   Goal: Test all possible combinations of condition outcomes within each predicate.
            *   Limitations: Can lead to an explosive number of test cases, often impractical and rarely mandated due to complexity and potential redundancy.
    *   **Path Coverage**:
        *   **All-Paths Coverage**: Execute every unique execution path from start to end.
            *   Limitations: Impractical due to path explosion in programs with loops (*e.g., N loops can lead to Factorial(N) or X^N paths*).
        *   **Independent Path Coverage** (_McCabe Complexity_):
            *   Goal: Cover a set of "linearly independent" paths, which represent all distinct ways of traversing the control flow graph.
            *   **McCabe Cyclomatic Complexity (V(G))**: A metric to calculate the number of independent paths. `V(G) = E - N + 2P` (Edges - Nodes + 2 * Components) or simpler, `V(G) = Number of Decision Points + 1`.
            *   Strength: A strong criterion that implies 100% Decision and Statement Coverage.
    *   **Loop Testing**: Specific strategies for testing loops:
        *   Bypass: Test where the loop is not entered.
        *   Single Pass: Test where the loop iterates exactly once.
        *   Multiple Passes: Test where the loop iterates typical, minimum, and maximum (if applicable) times.
        *   Nested Loops: Test from the innermost loop outwards.

3.  **Subsumption Hierarchy**
    A hierarchy illustrating which coverage criteria automatically satisfy (subsume) others if 100% coverage is achieved:
    *   Stronger criteria subsume weaker ones.
        *   MCDC implies CDC, Branch, and Statement coverage.
        *   Independent Path coverage implies Branch and Statement coverage.
        *   All-Paths coverage theoretically subsumes all other control flow criteria (but is impractical).

4.  **Challenges & Importance**
    *   "Good Enough" Coverage: While 100% is ideal, practitioners may accept lower percentages (*e.g., 80%*) if remaining code is rarely used, reviewed, or deemed low-risk. However, uncovered code is a potential source of undiscovered bugs.
    *   Fault Masking: Even 100% coverage doesn't guarantee fault detection, as specific test data might not expose a fault, or one fault's effect might mask another's.
    *   Tool Support: IDEs (_e.g., IntelliJ_ with `JaCoCo`, _Eclipse_ with `Emma`) provide built-in code coverage analysis tools to identify covered/uncovered lines and decision points. They also show "hits" (how often a line/branch was executed), which can help identify redundant tests for test suite optimization.
    *   Maintenance Cost: High coverage criteria often lead to larger, more complex test suites that are costly to maintain, especially with frequent code changes.

5.  **Homework 3: White Box Testing**
    *   Task: Analyze a given program.
    *   Steps:
        1.  Draw its Control Flow Graph (including start/end nodes).
        2.  Design a minimum set of test cases to achieve specific coverage levels (*e.g., 100% Statement, then increase Branch/Decision coverage*).
        3.  Use an IDE's built-in coverage tool to measure and verify your test suite's adequacy.
        4.  Discuss the relationship between achieved Statement and Branch coverage.

---
---

## V. Software Testing: State-Based, Random, and GUI Approaches

This lecture explores advanced black box testing techniques, including State Transition Testing for event-driven systems, Random Testing for generating diverse inputs, and an overview of GUI Testing principles.

1.  **State Transition Testing**
    *   Concept: Models system behavior as a sequence of states and transitions between them. Primarily a black box approach, derived from requirements or inferred system behavior.
    *   Key Elements:
        *   **States**: Specific conditions or modes of the system (*e.g., "Waiting for Card," "Wait for PIN," "Connected"*).
        *   **Events**: Inputs or actions that trigger a change of state (*e.g., "Insert Card," "Enter PIN," "Cancel"*).
        *   **Actions/Outputs**: Responses produced by the system during a transition.
        *   **Guards**: Conditions that must be met for a transition to occur (*e.g., "PIN is Valid"*).
        *   **State Transition Diagram (STD)** / **State Transition Table (STT)**: Visual or tabular representation of states, events, and transitions.
    *   Test Case Generation: Involves designing sequences of events/inputs to traverse specific paths through the STD.
    *   Coverage Criteria (analogous to White Box Coverage):
        *   All-States Coverage: Visit every state at least once (weakest).
        *   All-Transitions Coverage: Traverse every state transition at least once (stronger, comparable to Branch Coverage).
        *   Impossible Transitions/Failure States: Test scenarios that trigger unexpected events or lead to error states (*e.g., inserting a card while already in "connected" state*).
    *   Application: Highly effective for event-driven systems (*e.g., telecommunication, ATMs, vending machines*).

2.  **Random Testing**
    *   Concept: A black box approach that generates test inputs randomly to find defects. Often called "Monkey Testing" for its seemingly unstructured nature.
    *   Random Number Generation: Typically uses pseudo-random number generators (*e.g., Linear Congruential Formula*) for reproducibility (same "random" sequence can be generated with the same seed).
    *   Effectiveness:
        *   Good at finding crash bugs or obvious failures.
        *   Can be inefficient for finding deeply hidden, specific faults that require very particular input combinations (low probability of hitting the "buggy spot" randomly).
        *   Effectiveness increases with the volume of tests run.
    *   Challenges:
        *   Complex Input Data Structures: Generating valid random inputs for complex data types (*e.g., objects, structured data*) requires mapping to simpler forms (like bit strings) and validation.
        *   Test Sequences: Generating meaningful sequences of actions (*e.g., for a stack: Push, Push, Pop*) is more complex than single random inputs. Tools like `Randoop` can generate these sequences.
        *   Test Oracle Problem (Major Challenge): The biggest hurdle – how to automatically determine if a randomly generated output is correct or incorrect?
            *   Often relies on crash detection.
            *   May use plausibility checks (*e.g., "absolute value must be positive"*).
            *   Comparison against a "golden" (known good) version of the software.
    *   **Intelligent Random Testing** / **Fuzzing**:
        *   More sophisticated random testing that uses feedback (*e.g., code coverage information from white box analysis*) to guide the random input generation towards unexercised code paths, increasing bug-finding efficiency.
        *   Fuzzers are tools for intelligent random testing.
    *   **Homework 4** (Random Testing): You will use `EvoSuite` (an evolutionary algorithm-based tool) to automatically generate unit tests for a given program. The assignment focuses on comparing the quality and behavior of automatically generated tests versus manually written tests, especially in the presence of bugs and refactoring.

3.  **GUI Testing** (_Graphical User Interface_)
    *   Concept: Focuses on testing the user interface of an application.
    *   Methods:
        *   **GUI Ripping**: Tools automatically analyze the GUI structure (windows, widgets, attributes) at runtime.
        *   **Event Flow Graph**: A model (similar to STD) representing possible interactions and transitions between GUI elements.
        *   Automated Action Generation: Tools generate sequences of user actions (clicks, text input, scrolling).
    *   Tools Mentioned:
        *   `GUITAR` / `TESTAR`: Generate event sequences for robustness testing. Can use filters (*e.g., avoid repeated "close" button clicks*) and basic oracles (*e.g., detect suspicious text in titles*).
        *   `Sikuli`: An image-based GUI testing tool. Instead of explicit element IDs, it uses images of GUI elements to locate and interact with them.
    *   Challenges:
        *   Oracle Problem: Difficult to define what constitutes a "correct" visual or interactive state (*e.g., layout, responsiveness, animations*).
        *   Image-Based Issues (`Sikuli`): Sensitivity to screen resolution, minor visual changes, or similar-looking elements can break tests.
        *   Non-Deterministic Behavior: GUI interactions can be complex and user-dependent.
        *   Limited Business Logic Testing: GUI tools primarily test the UI layer, not the underlying business logic.

---
---

## VI. Software Testing: Levels, Automation & Advanced Techniques

This lecture covers the hierarchical structure of software testing, the principles and benefits of test automation, and delves into specialized techniques like integration testing with mocking, data-driven approaches, and model-based testing.

1.  **Test Levels Hierarchy**
    Software testing is typically conducted at different levels, each with a distinct focus and purpose:
    *   **Unit Testing**:
        *   Focus: Individual, smallest testable components (classes, methods).
        *   Who: Developers.
        *   Approach: Primarily White Box (structural).
        *   Goal: Verify internal logic and functionality in isolation.
        *   Tools: `JUnit` (Java), etc.
    *   **Integration Testing**:
        *   Focus: Interactions and interfaces between integrated units/components.
        *   Who: Developers.
        *   Approach: Mix of White Box and Black Box.
        *   Goal: Verify collaboration and data flow between modules.
        *   Strategies: Bottom-up, top-down, hybrid (sandwich), or Big Bang (rarely recommended).
    *   **System Testing**:
        *   Focus: The complete, integrated system as a whole.
        *   Who: Independent test teams, external consultants.
        *   Approach: Primarily Black Box (specification-based).
        *   Goal: Verify functional and non-functional requirements (performance, security, usability, reliability) in a production-like environment.
    *   **Acceptance Testing**:
        *   Focus: System readiness for release, meeting business needs in the user's environment.
        *   Who: Customers, end-users, business representatives.
        *   Types:
            *   Alpha Testing: Done in the development organization's environment by internal "users."
            *   Beta Testing: Done by real end-users in their own environment.
        *   Goal: Final validation that the system meets user expectations and business objectives.
    *   Agile Context: Test levels are not strict waterfall phases. In Agile, testing is continuous and integrated into sprints, with frequent unit, integration, and even system-level checks (*e.g., daily unit tests, sprint-end stabilization phases*).

2.  **Integration Testing with Mocking**
    *   Problem: When testing a unit that depends on other units (*e.g., external services, database, other classes*), these dependencies might not be ready, or you want to isolate your unit's test from their potential bugs/unpredictability.
    *   Solution: **Mocking/Stubbing**: Creating "fake" or "simulated" versions of dependent objects/services.
        *   **Mock** (`Mockito`, `JMockit`): A configurable object that doesn't have the real implementation but can be programmed to return specific values or perform defined actions when its methods are called.
            *   `@Mock`: Annotation to create a mock object.
            *   `when(mock.method()).thenReturn(value)`: Defines the mock's behavior.
            *   `verify(mock).method()`: Checks if/how many times a mocked method was called.
        *   **Spy**: A partial mock; a real object whose methods can still be selectively mocked, allowing for a mix of real and simulated behavior.
    *   Benefits: Isolates the unit under test, enables parallel development, simplifies testing of complex dependencies, helps pinpoint the source of integration bugs.

3.  **Test Automation**
    *   Scope: Automation can apply to various testing activities, not just execution:
        *   Test Design/Generation: Tools create test cases/data (*e.g., combinatorial testing tools like `ACTS`, evolutionary tools like `EvoSuite`*).
        *   Test Scripting: Writing executable tests (*e.g., `JUnit` for unit, `Selenium` for web UI*).
        *   Test Execution: Running the tests automatically.
        *   Test Evaluation/Reporting: Analyzing results, logging failures, generating reports.
        *   Debugging Support: Tools aiding in fault localization.
    *   Advantages:
        *   Efficiency: Faster and repeatable execution (especially for regression testing).
        *   Scalability: Enables testing large systems or complex configurations.
        *   Robustness: Consistent and unbiased execution.
        *   Compliance: Provides documented proof of testing for legal/regulatory purposes.
    *   Disadvantages:
        *   Maintenance Cost: Automated tests require maintenance as software evolves (similar to production code).
        *   Oracle Problem: Tools often generate inputs but cannot automatically determine the correct expected output.
        *   Limited Scope: Cannot replace all human-led testing (*e.g., exploratory testing, complex usability issues, highly subjective quality aspects*).
        *   False Sense of Security: High automation coverage doesn't guarantee a bug-free product.
    *   AI/LLMs in Testing: Emerging field, promising for generating test code and potentially even test oracles, reducing manual effort in test design.

4.  **Web Application Testing Tools (`Selenium`)**
    *   `Selenium`: A widely used framework for automating web browsers.
    *   Scripting: Involves writing code to simulate user interactions (clicks, text input, navigation).
    *   Element Location: Key challenge is identifying web elements (*e.g., by ID, XPath, link text*). Browser implementations can vary, affecting element location.
    *   Capture-Replay Tools: Record manual user actions and generate scripts for replay. Convenient for initial setup but often brittle and hard to maintain with UI changes.
    *   Engineered Scripts: Manually written scripts using `Selenium` API. More robust and maintainable.
    *   **Data-Driven Testing**:
        *   Concept: Separating test data (inputs, expected outputs) from the test logic. Data is stored externally (*e.g., Excel, CSV*).
        *   Benefits: Increases flexibility, reusability of test scripts, allows non-technical users (*e.g., domain experts, business analysts*) to contribute test data.
    *   **Keyword-Driven Testing**:
        *   Concept: Extends data-driven testing by adding a layer of abstraction. Test steps are defined by "keywords" (*e.g., "Login," "Add Item"*), which are then mapped to specific actions and data.
        *   Benefits: Further abstracts test cases from code, enabling non-technical users to design higher-level tests.

5.  **Model-Based Testing** (_Behavioral Models_)
    *   Concept: Uses a behavioral model of the system (often an event flow graph or state chart) to automatically generate test sequences/paths.
    *   Tool (`GraphWalker`): Takes a model (*e.g., a GUI's event flow graph*) and traverses it to generate sequences of actions (clicks, inputs).
    *   Benefits: Systematic exploration of system behavior, efficient generation of diverse test paths.
    *   Limitations: Primarily for crash testing or detecting unexpected behavior; still faces the test oracle problem (determining correct outputs).

6.  **Homework 5: Web Application Testing with `Selenium`**
    *   Task: Automate testing of a given web application using `Selenium`.
    *   Focus: Writing engineered test scripts, applying principles of positive/negative testing, and demonstrating understanding of automated test design for web UIs.

---
---

## VII. Software Testing: Advanced Black Box Techniques

This lecture delves into specialized black box testing methods beyond basic functional checks, focusing on situations where traditional testing is difficult or insufficient.

1.  **Metamorphic Testing (MT)**
    *   Core Idea: Testing software systems where the expected output is unknown or impractical to determine for every input (*e.g., scientific calculations, simulations, optimization problems, AI/ML systems*).
    *   How it Works:
        *   Identify a **Metamorphic Relation (MR)**: A property describing how the output of a system should change (or remain unchanged) when the input is transformed in a specific, predefined way.
        *   Provide an initial Input (I1) to the System Under Test (SUT) to get Output (O1).
        *   Transform I1 into a Follow-up Input (I2) based on the MR.
        *   Provide I2 to the SUT to get Output (O2).
        *   Check if the relationship between O1 and O2 satisfies the defined MR.
    *   Example (Google Maps):
        *   MR: Swapping origin (S) and destination (E) coordinates should result in the same distance and travel time (though the path direction is reversed).
        *   If SUT gives different results for S-E vs. E-S, it indicates a potential bug, without knowing the absolute correct distance.
    *   Application to AI/ML: Highly useful for testing AI models (*e.g., image recognition, autonomous driving perception*).
        *   MR Example: If an object detection system correctly identifies a "STOP" sign in an image, it should still identify it if the image is slightly blurred, rotated, or has minor pixel changes. (Output remains unchanged).
        *   Tools like `DeepTest` apply systematic image transformations to test AI robustness.
    *   Challenges:
        *   Designing Strong MRs: It's non-trivial to identify robust MRs that are likely to expose faults. Requires deep domain knowledge of the SUT's properties.
        *   Automating MR Discovery: An active research area.
        *   Applicability: More challenging for non-functional properties like usability or performance.
    *   Homework Connection: You will apply MT to test a braking distance calculator and a traffic sign recognizer, where the "best" version is found by identifying robust behavior under various metamorphic transformations (*e.g., simulating different weather conditions*).

2.  **Security Testing**
    *   Goal: Identify security vulnerabilities in software and prevent unauthorized access, data breaches, or system compromise.
    *   Key Principles (CIA Triad + AAA+N):
        *   Confidentiality: Preventing unauthorized disclosure of information.
        *   Integrity: Preventing unauthorized modification or destruction of data.
        *   Availability: Ensuring systems and data are accessible when needed.
        *   Authentication: Verifying user identity.
        *   Authorization: Defining and enforcing user permissions.
        *   Accountability: Tracing actions to responsible entities.
        *   Non-repudiation: Preventing denial of actions.
    *   Common Practices:
        *   Vulnerability Scanning: Automated tools to identify known weaknesses (static analysis, dynamic analysis).
        *   Security Scanning: Analyzing system behavior during runtime for suspicious activities.
        *   Penetration Testing: Ethical hackers simulate real-world attacks to find exploitable vulnerabilities.
        *   Risk Assessment & Auditing: Evaluating potential threats and adherence to security policies.
    *   Common Vulnerabilities (OWASP Top 10): Examples like SQL Injection (*e.g., bypassing login with malicious SQL queries*).
    *   Guest Lecture: Christina Rakema will cover security testing for mobile applications in more detail.

3.  **Usability Testing**
    *   Goal: Evaluate how easy, efficient, and satisfying a software system is to use.
    *   Criteria Examples: Learnability, efficiency, memorability, error prevention, user satisfaction, accessibility.
    *   Evaluation Methods:
        *   Inspection-based (Cheaper):
            *   Cognitive Walkthrough: Experts simulate user tasks to find usability issues.
            *   Heuristic Evaluation: Experts assess the UI against established usability principles (*e.g., Nielsen's 10 Heuristics: Visibility of system status, Match between system and real world, User control & freedom, Consistency & standards, Error prevention, Recognition rather than recall, Flexibility & efficiency of use, Aesthetic & minimalist design, Help users recognize/diagnose/recover from errors, Help & documentation*).
            *   Review Guidelines: Checking against detailed design rules.
        *   User-based (More Expensive):
            *   Laboratory Experiments: Users perform tasks in a controlled environment, observed by researchers.
            *   Field Studies: Users interact with the system in their natural environment.
    *   Data Collection: Observation, think-aloud protocols, keystroke logging, questionnaires, interviews.
    *   Design Principles (for UI): Proximity, Alignment, Repetition, Contrast.

4.  **A/B Testing**
    *   Concept: A controlled experiment to compare two or more versions (A, B, etc.) of a UI element or feature to determine which performs better against a specific metric.
    *   How it Works: Different user segments (randomly assigned) are exposed to different versions, and their interactions are monitored.
    *   Applications:
        *   Marketing/E-commerce: Optimize website elements (button text, images, pricing) to increase conversion rates (*e.g., sales, sign-ups*).
        *   Politics: Optimize campaign messages or website layouts to increase engagement (*e.g., donations, volunteer sign-ups*).
        *   Product Development: Validate new features or design changes.
    *   Benefits: Data-driven decision making, direct measurement of user impact.
    *   Scalability: Can be extended to A/B/C/D... (multivariate testing) for many variations, though this complicates analysis.
    *   Internal AI Testing (Google's approach): Simulating A/B testing internally during development to identify impactful weaknesses in AI components before external release.

---
---

## VIII. Mobile Application Security Testing: Identifying & Mitigating Vulnerabilities

This lecture, given by Christina, focuses on understanding, rating, and testing software vulnerabilities, particularly within mobile applications, guided by OWASP principles.

1.  **Understanding Vulnerabilities & Attacks**
    *   **Vulnerability**: A weakness or flaw in software that can be exploited.
    *   **Attack**: An unauthorized action taken by an attacker to exploit a vulnerability, manipulating the application for unintended purposes (*e.g., gaining root access, stealing data*).
    *   **Vulnerability Rating** (`CVSS` - Common Vulnerability Scoring System): A standardized system to quantify vulnerability severity, using:
        *   Exploitability Metrics:
            *   Attack Vector: How the attack is launched (*e.g., Network, Local, Physical*).
            *   Attack Complexity: Difficulty of the attack (*e.g., High – requires man-in-the-middle; Low – easily exploitable*).
            *   Privileges Required: Attacker's access level needed (*e.g., None, Low, High*).
            *   User Interaction: If the victim must perform an action (*e.g., click a link*).
        *   Impact Metrics: Consequences on the affected system:
            *   Confidentiality: Unauthorized data disclosure.
            *   Integrity: Unauthorized data modification.
            *   Availability: Disruption of service/data access.

2.  **OWASP** (_Open Web Application Security Project_)
    *   Role: A non-profit foundation dedicated to improving software security across all types of applications (web, mobile, desktop).
    *   **OWASP Top 10 Lists**: Annually updated lists of the most critical and common security risks, providing a prioritized focus for developers.
        *   Web Top 10 (Examples): Broken Access Control, Cryptographic Failures, Injections (SQLi), Insecure Design, Vulnerable & Outdated Components.
        *   Mobile Top 10 (2016 version discussed): Focus of this lecture.
        *   Desktop Top 10: Similar concepts but with specific risks for offline functionality and broader system access.

3.  **Mobile App Security Testing Approaches**
    *   With Source Code (White Box): Easier to review code for secure practices, data handling, and correct API usage.
    *   Without Source Code (Black Box / Gray Box): More complex, often used for third-party apps. Requires:
        *   Device Rooting/Jailbreaking: Gaining full access to the device's file system (easier on Android, harder on iOS).
        *   Tools:
            *   `Frida`: Dynamic instrumentation toolkit for iOS/Android; allows runtime memory debugging, method hooking, and custom code execution for advanced testing (*e.g., fuzzing*).
            *   `ADB` (Android Debug Bridge): Command-line tool for Android device interaction.
    *   OWASP Mobile Security Resources:
        *   **Mobile Security Testing Guide (MSTG)**: Comprehensive open-source guide for mobile app security testing.
        *   **Mobile AppSec Verification Standard (MASVS)**: Defines security requirements for mobile apps, categorized into levels.
    *   **MASVS Security Levels**:
        *   L1 (Standard Security): For apps with minimal sensitive data (*e.g., simple games*).
        *   L2 (Defense in Depth): For apps handling sensitive data (*e.g., banking, health*). Requires strong data protection.
        *   R (Resilience against Reverse Engineering & Tampering): Additional protection for apps where preventing understanding or modification of logic is critical (*e.g., multiplayer games to prevent cheating, banking apps to prevent client-side fraud*).

4.  **OWASP Mobile Top 10 Risks** (with Examples)
    *   M1: Improper Platform Usage: Misusing or failing to correctly use platform-provided security features (*e.g., Android Intents, iOS Keychain*).
        *   Example (TikTok): Unverified Android Intent inputs allowed malicious apps to access TikTok files and run arbitrary code. Prevention: Input sanitization, following platform best practices.
    *   M2: Insecure Data Storage: Unintended data leakage due to improper local storage.
        *   Example (Tinder/Bumble): Sending exact user coordinates to the client, allowing triangulation of user location. Prevention: Enforce security controls on the server-side, not just client-side, and only send necessary data.
    *   M3: Insecure Communication: Vulnerabilities in network traffic (*e.g., cleartext, improper SSL/TLS usage*).
        *   Example (Think Mutual Bank App): Lack of proper SSL certificate verification allowed credential capture over the same network. Prevention: Certificate pinning, using trusted libraries, dynamic analysis.
    *   M4: Insecure Authentication: Flaws in user identity verification or session management.
        *   Example (CRAB Android app): No brute-force protection on 4-digit PIN bypass for 2FA. Prevention: Brute-force detection on remote endpoints, stronger authentication tokens.
    *   M5: Insufficient Cryptography: Weak or improperly applied encryption.
        *   Example (OLAP): Decryption key embedded directly in the app's code, easily extractable via reverse engineering. Prevention: Never embed keys in code, use secure key management, follow NIST guidelines.
    *   M6: Insecure Authorization: Allowing authenticated users to perform privileged actions they shouldn't (distinct from authentication).
        *   Example (Children's Smartwatches): IDOR (Insecure Direct Object Reference) allowed changing user IDs in requests to access other children's GPS data, calls, and audio. Prevention: Server-side validation of incoming identifiers against current user's authorization.
    *   M7: Client Code Quality: General code-level implementation problems (*e.g., buffer overflows, memory leaks, format string vulnerabilities*).
        *   Example (WhatsApp): Specially crafted packets in a call could trigger a buffer overflow, allowing arbitrary code execution and spyware installation. Prevention: Secure memory management, code reviews, static analysis, using memory-safe languages.
    *   M8: Code Tampering: Exploiting code modifications (*e.g., binary patching, method hooking, dynamic memory modification*).
        *   Example (Pokemon Go): Users spoofed GPS data to bypass walking requirements and find rare Pokémon. Prevention: Root/jailbreak detection, integrity checks on executable files and critical data within the sandbox.
    *   M9: Reverse Engineering: Revealing intellectual property or sensitive information by decompiling code.
        *   Prevention: Code obfuscation (makes understanding harder but not impossible).
    *   M10: Extraneous Functionality: Presence of unwanted or hidden functionality (*e.g., hidden backdoors, test-only features left in production*).
        *   Example (Wi-Fi File Transfer): App opened an unauthenticated port, giving full access to the device. Prevention: Secure code reviews, threat modeling, proper architecture design, rigorous removal of temporary/dev features.

5.  **General Mobile Security Controls** (OWASP Recommendations)
    *   Protect sensitive data on device and in transit.
    *   Handle credentials securely (use platform-provided mechanisms).
    *   Implement correct authentication, authorization, and session management (server-side checks are crucial).
    *   Secure backend APIs and services.
    *   Secure data integration with third-party services.
    *   Pay attention to user data collection and privacy.
    *   Implement controls for paid-for resources (*e.g., in-app purchases, SMS*).
    *   Ensure secure distribution/provisioning (supply chain security).
    *   Carefully check runtime code interpretation for errors (*e.g., memory errors*).

Motivation: Security testing is crucial. Understanding common vulnerabilities and prevention methods is vital for all developers, even if they aren't dedicated security testers.

---
---

## IX. Software Testing: Data Flow & Mutation Analysis

This lecture covers two advanced White Box testing techniques: Data Flow Testing (DFT), which focuses on variable usage, and Mutation Testing (MT), which assesses the effectiveness of a test suite itself.

1.  **Data Flow Testing (DFT)**
    *   Concept: A white box testing approach that aims to cover specific paths related to the definition and use of variables within a program's control flow. It's stronger than basic control flow coverage criteria (like statement or branch coverage).
    *   Motivation:
        *   Control flow graphs mainly focus on path execution, but not on what happens with data/variables along those paths.
        *   Can expose "data flow anomalies" (*e.g., variable defined but never used, or used before defined*).
    *   Key Terminology:
        *   **Definition (d)**: A point in the code where a variable is assigned a value (*e.g., `x = 10;`, `int y;`*).
        *   **Use (u)**: A point in the code where a variable's value is accessed.
            *   **Computational Use** (_c-use_): Used in a calculation or expression (*e.g., `y = x + 5;`*).
            *   **Predicate Use** (_p-use_): Used in a decision-making condition (*e.g., `if (x > 0)`*).
        *   **Definition-Use (DU) Pair**: A pair (d, u) where d is a definition of a variable and u is a use of the same variable.
        *   **Definition-Clear Path**: A path from a definition d to a use u where the variable is not redefined anywhere else along that path. This is crucial to avoid testing irrelevant redefinitions.
    *   **Data Flow Coverage Criteria** (from weakest to strongest):
        *   **All Definitions** (_All Defs_): Cover at least one definition-clear path from each definition of a variable to any of its uses. (Weakest DFT criterion, often covered by basic branch coverage).
        *   **All Uses**: Cover at least one definition-clear path from each definition of a variable to every one of its uses.
        *   **All Definition-Use Paths** (_All DU Paths_): Cover all definition-clear paths from each definition of a variable to each of its uses. (Strongest DFT criterion, computationally expensive).
    *   Relationship to Control Flow: DFT criteria generally subsume (are stronger than) statement and branch coverage. Empirical studies have shown that achieving a high percentage of DU coverage can find more seeded faults than achieving the same percentage of branch coverage, though it requires more tests.
    *   Special Case: Loops: Loops can complicate DU path analysis due to repeated redefinitions. The "definition-clear path" concept helps manage this by focusing on single-definition-to-use flows within or across loop iterations.
    *   Tool Support: Modern IDEs (_e.g., IntelliJ_) offer some built-in support for data flow analysis.

2.  **Mutation Testing (MT)**
    *   Concept: A technique used to evaluate the quality and strength of a test suite, rather than directly finding bugs in the production code. It assesses how well a test suite can detect intentionally introduced faults.
    *   Analogy: Inspired by biological mutation. Small, deliberate changes (mutations) are introduced into the code to create "**mutants**."
    *   Process:
        *   Start with the original program and an existing test suite (all tests must pass on the original program).
        *   Generate Mutants: Create numerous slightly modified versions of the program. Each mutant contains a single, small, artificial fault (*e.g., changing `+` to `-`, `>` to `>=`*). These changes are defined by **mutation operators**.
        *   Run the test suite against each mutant.
        *   **Killed Mutant**: If at least one test in the suite fails when run against a mutant, that mutant is "killed." This indicates the test suite is strong enough to detect that specific fault.
        *   **Live Mutant**: If all tests in the suite pass when run against a mutant, that mutant is "live." This indicates a weakness in the test suite – it failed to detect the introduced fault.
        *   **Mutation Score**: The percentage of killed mutants (higher is better). A high score suggests a strong test suite.
    *   Types of Mutants:
        *   **Trivial Mutants**: Easily detectable (*e.g., syntax errors, obvious logic flaws*). Not very useful for assessing test suite strength.
        *   **Equivalent Mutants**: Mutants that produce exactly the same output as the original program for all possible inputs. Cannot be killed by any test. These are problematic as they artificially lower the mutation score and are hard to detect automatically.
    *   Mutation Operators: Define the types of changes to create mutants (*e.g., changing arithmetic operators, relational operators, logical operators, variable names, deleting statements*). They aim to mimic common programming mistakes.
    *   Application: Regularly used by major software companies for regression testing to ensure test suites remain effective as code evolves.

3.  **Homework 6** (Mutation Testing)
    *   Task: Use a mutation testing tool (`PIT`) on a MinimumBinaryHeap program.
    *   Activities:
        1.  Generate mutants of the given code.
        2.  Run provided tests and analyze the initial mutation coverage.
        3.  Improve the test suite by adding new tests to "kill" more live mutants.
        4.  Compare mutation coverage with traditional code coverage metrics.
        5.  Document the process and rationale for test improvements.

---
---

## X. Software Testing: Advanced White Box & Static Analysis

This lecture delves into Symbolic Execution as a path-coverage technique, explores Static Code Analysis tools for automated defect detection, and discusses the importance and methodologies of Manual Inspections and Reviews for comprehensive quality assurance.

1.  **Symbolic Execution**
    *   Concept: A white box testing technique that generates test data by analyzing the program's control flow and solving constraints on input variables.
    *   Goal: To systematically achieve high code coverage (*e.g., branch coverage, path coverage*) by determining specific inputs that force execution along desired paths.
    *   Process:
        *   Represent program inputs as symbolic variables (*e.g., `x` instead of `5`*).
        *   As execution proceeds symbolically, collect path constraints from predicates (conditions in `if`, `while` statements).
        *   For a chosen execution path, solve the accumulated path constraints using a constraint solver.
        *   If a solution exists, it represents concrete input values that will execute that specific path.
    *   Benefits: Can generate test data for hard-to-reach code paths; helps guarantee specific coverage criteria.
    *   Challenges:
        *   Path Explosion: The number of paths can be very large (especially with loops), making it computationally intensive.
        *   Complex Constraints: Solving complex mathematical or logical constraints can be difficult or slow.
        *   External Dependencies: Handling inputs from external components (*e.g., user input, network calls*) is complex.
    *   Tools: `Key Project` (symbolic execution debugger), `Java Pathfinder`.

2.  **Static Code Analysis**
    *   Concept: Analyzing source code (or sometimes object code) without executing it to find potential defects, vulnerabilities, or bad coding practices.
    *   Goal: Proactively identify issues early in the development cycle.
    *   Common Issues Detected:
        *   Null Pointer Exceptions: Dereferencing a null reference (*e.g., accessing `x.method()` when `x` is null*). Tools trace potential null assignments to their usage.
        *   Uninitialized Variables: Using a variable before it has been assigned a value.
        *   Resource Leaks: Opened files, network connections, or database connections not properly closed.
        *   Security Vulnerabilities: Known patterns of insecure coding (*e.g., SQL injection vulnerabilities, cross-site scripting*).
        *   Bad Practices / Code Smells: Code that is overly complex, redundant, or hard to maintain.
    *   Tools:
        *   `SpotBugs` (formerly `FindBugs`): A static analyzer for Java that identifies various bug patterns.
        *   `SonarQube`: A broader platform that includes static analysis, code quality metrics, and security vulnerability detection for multiple languages.
    *   Challenges:
        *   False Positives: Warnings that are reported as potential problems but are not actual defects in specific contexts. (A major challenge, requires human review).
        *   False Negatives: Actual defects that the tool fails to detect.
        *   Context Dependency: Tools might struggle with dynamic behavior, external inputs, or inter-component interactions.
    *   Homework Connection: You will use `SpotBugs` to analyze a program, identify potential issues (warnings), and determine whether they are true positives or false positives based on argumentation.

3.  **Manual Static Analysis: Inspections and Reviews**
    *   Concept: Human-driven examination of software artifacts (documents, code) to identify defects.
    *   Purpose: Complement automated testing and static analysis by leveraging human understanding, domain knowledge, and different perspectives. Often focuses on readability, maintainability, and conceptual correctness.
    *   Artifacts to Review: Requirements, design documents, source code, test plans, user manuals.
    *   **Fagan Inspections** (Historical, 1970s IBM): A formal, multi-stage, team-based inspection process that significantly improved software quality by finding defects early.
        *   Phases: Planning, Overview, Preparation, Inspection Meeting, Rework, Follow-up.
        *   Key Idea: Finding defects early (*e.g., in requirements or design*) is significantly cheaper than fixing them later (*e.g., after deployment*).
    *   **Modern Review Techniques**:
        *   Ad-hoc Reading: Informal, quick review.
        *   Checklist-based Reading: Guided by a list of common issues or standards.
        *   Defect-based Reading: Focused on finding types of defects known from past projects.
        *   Usage-based Reading: Prioritizing review based on how a document will be used in subsequent development phases.
        *   **Perspective-based Reading (PBR)**: Different roles (*e.g., developer, tester, user*) review the same artifact from their unique viewpoint, leading to the detection of different types of problems.
    *   Defect Metrics:
        *   Effectiveness: (Defects Found / Total Defects in artifact) * 100%.
        *   Efficiency: (Defects Found / Effort Spent).
        *   Cost of Defects: Exponentially increases the later a defect is found (*e.g., requirements bug found during usage is 50x-200x more expensive than if found during requirements review*).
    *   Tools for Code Review: `Gerrit` (for version control integration), often integrated into IDEs or CI/CD pipelines for comments and voting on changes.
    *   **Defect Prediction Models** (Future Lecture): Using data from reviews (*e.g., problems found by different perspectives, defect types*) to predict remaining defects in artifacts. (Often uses ecological models like capture-recapture).

---
---

## XI. Software Testing: Quality Estimation & Process Improvement

This lecture focuses on assessing software quality before delivery, particularly through quality estimation models and the structured practice of inspections and reviews. It also touches upon test organization and process maturity.

1.  **Quality Estimation: Predicting Defects & Quality**
    *   Goal: To predict the quality of a software product (*e.g., number of remaining faults, expected failures, effort to fix problems*) to decide if it's "good enough" for release.
    *   Challenge: Quality is multifaceted (correctness, maintainability, security, performance) and difficult to measure directly. Prediction relies on quantifiable measures and data.
    *   Types of Predictions:
        *   Number of Faults/Failures: How many bugs/failures are still undetected? How many will be found in future usage?
        *   Faulty vs. Non-Faulty Modules: Classifying modules/classes as likely to contain faults (binary classification).
        *   Issue Resolution Time/Effort: How long/much effort will it take to fix a detected problem?
        *   Impact of Changes: Predicting effects of refactoring on quality attributes (*e.g., energy consumption, performance*).
    *   Modeling Techniques: Often statistical (regression, classification models), drawing from past project data (labeled datasets) and product/process characteristics.

2.  **Review Techniques for Defect Estimation**
    *   Reviews and inspections are manual static analysis techniques used to find defects in software artifacts (requirements, design, code, test plans).
    *   **Types of Reading/Reviewing Techniques**:
        *   Ad-hoc Reading: Unstructured, informal.
        *   Checklist-based Reading: Guided by a predefined list of potential issues. Can be enhanced by Defect-based Reading (checklists derived from historical common defects).
        *   Usage-based Reading: Focuses on reviewing parts of the artifact that correspond to high-priority user scenarios or expected usage. (Often more effective for critical defects).
        *   **Perspective-based Reading (PBR)**: Different roles (*e.g., developer, tester, end-user*) review the same artifact from their unique viewpoint, finding different types of problems. This is key for defect estimation.
    *   Defect Metrics:
        *   Effectiveness: (Number of Defects Found / Total Defects in Artifact) * 100%.
        *   Efficiency: (Number of Defects Found / Effort Spent).
        *   Cost of Defects: Defects found earlier in the development lifecycle are significantly cheaper to fix than those found later (*e.g., by end-users*).
    *   **Capture-Recapture Modeling** (for Undetected Defects):
        *   Analogy: Used in ecology to estimate animal populations (catch, tag, release, re-catch).
        *   Application to Software:
            *   Each independent reviewer (inspector) acts as a "capture" round.
            *   Overlap in defects found by different reviewers indicates the "recaptured" items.
        *   Core Idea: The more overlap (duplicates) found by different independent reviewers, the fewer estimated remaining defects. The less overlap, the more estimated remaining defects (tends towards infinity if no overlap).
        *   Simplified Formula (2 Reviewers):
            *   Estimated Total Defects (NT) = `(D1 * D2) / D12` (where D1 = Defects found by Reviewer 1, D2 = Defects found by Reviewer 2, D12 = Defects found by both).
            *   Estimated Remaining Defects (NR) = `NT - (D1 + D2 - D12)` (where NR = Estimated Number of Remaining Defects).
        *   Assumptions: Reviewers work independently (no influence), defects are not fixed during the review period. More complex models account for reviewer abilities and defect difficulty.
        *   Homework Connection: You will apply the capture-recapture model to estimate remaining defects in a specification document after a collaborative review.

3.  **Test Documentation & Organization**
    *   Test Documentation (IEEE Standards exist):
        *   Test Plan: Outlines scope, strategy, resources, and schedule (often simplified in agile contexts).
        *   Test Case Specification: Defines inputs, expected outputs, and execution conditions for individual tests.
        *   Test Incident Report (Issue Report): Documents observed failures, including reproduction steps, actual vs. expected results, and context.
        *   Test Summary Report: Summarizes testing activities and results.
    *   **Test Organization Structures** (Increasing Complexity/Size):
        *   Developers perform all testing: Small teams, shared responsibility.
        *   Dedicated Testers within Teams: Specialized testers embedded in development teams.
        *   Independent Test Team/Group: Separate department/group for testing (system/acceptance).
        *   Central Quality Assurance Group: Enterprise-level QA oversight.
        *   Outsourced Testing: Third-party companies (*e.g., TestLeo*) provide testing services.
        *   Crowdsourced Testing: Utilizing a large, diverse group of external testers.
    *   Challenges in Test Organization: Maintaining communication, avoiding "us vs. them" mentality between developers and testers, managing power dynamics, ensuring clear responsibilities.

4.  **Test Process Improvement & Maturity Models**
    *   Goal: Systematically improve the effectiveness and efficiency of software testing processes.
    *   Process Analysis: Analyzing collected defect data (types, injection points, detection points, fix costs) to identify root causes and areas for improvement. This contributes to a "learning organization."
    *   **Test Maturity Models** (`TMM`, `CMM`, `SPICE`): Frameworks to assess an organization's maturity level in its testing processes.
        *   Levels (typically 1 to 5):
            *   Level 1 (Initial): Ad-hoc, chaotic testing.
            *   Level 2 (Managed): Basic documented processes, foundational tools (planning, automation).
            *   Level 3 (Defined): Standardized, organization-wide processes.
            *   Level 4 (Quantitatively Managed): Processes are measured and controlled, data-driven decisions.
            *   Level 5 (Optimizing): Continuous improvement based on feedback and quantitative analysis.
    *   Relevance: Helps organizations identify their current testing capabilities and plan steps for systematic enhancement.

---
---

## XII. Software Testing: Quality Estimation, Process Improvement & Exam Prep

This final lecture covers advanced topics in quality estimation (predicting remaining defects), revisits review techniques, and discusses test organization and process maturity. It concludes with a comprehensive exam preparation guide.

1.  **Quality Estimation: Predicting Defects**
    *   Goal: Assess software quality before release by estimating the number of remaining faults or predicting future failures.
    *   Challenge: Quality is hard to measure and predict; relies on collected data.
    *   Methods of Estimation:
        *   Based on Detected Faults: Predict total/remaining faults from those already found.
        *   Based on Product Characteristics: Predict faults based on code size, complexity, change frequency (churn).
        *   Based on Process/People: Predict fix effort or time based on development process or developer experience.
    *   **Reliability Growth Models** (Historical):
        *   Concept: Statistical models that plot cumulative failures found over time/effort to predict when testing can stop (*e.g., when 95% of failures are found*).
        *   Types: Exponential (predicts asymptote for total failures), S-shaped (accounts for initial setup phase), Logarithmic (no asymptote, more flexible for changes).
        *   Limitations: Often rely on unrealistic assumptions (*e.g., no defects fixed during testing*) and are less used in modern continuous delivery environments.
    *   Key Approach: **Capture-Recapture Modeling**:
        *   Concept: Borrowed from ecology (estimating animal populations).
        *   Application: Used with Perspective-Based Reading (PBR). Multiple independent reviewers (*e.g., developer, tester, user*) examine the same artifact, each acting as a "capture" session for defects.
        *   Principle: The more overlap (common defects) found by different reviewers, the fewer estimated remaining undetected defects. The less overlap (more unique defects found by each), the more estimated remaining defects.
        *   Formula (for 2 reviewers):
            *   Estimated Total Defects (NT) = `(D1 * D2) / D12` (D1 = defects by reviewer 1, D2 = defects by reviewer 2, D12 = shared defects).
            *   Estimated Remaining Defects (NR) = `NT - (D1 + D2 - D12)` (Subtract unique found defects from total estimate).
        *   Assumptions: Reviewers work independently, defects are equally likely to be found (often simplified).
        *   Homework Connection: You will apply this model to a document review task.

2.  **Review Techniques** (Recap & Deep Dive)
    *   Review Goal: Find errors of commission (wrong, ambiguous, inconsistent) and omission (missing).
    *   Types of Reading:
        *   Ad-hoc: Unstructured.
        *   Checklist-based: Guided by a general list of issues.
        *   Defect-based: Guided by a list of past common defects from the organization.
        *   Usage-based: Focus on areas related to specific user scenarios.
        *   Perspective-based (PBR): Different stakeholders review from their unique viewpoint.
    *   Effectiveness: Usage-based reading often better for critical defects; checklist-based for less critical ones. PBR is powerful because different perspectives uncover different problem types.
    *   Benefits of Reviews (Beyond Defect Finding): Knowledge sharing, joint code ownership, learning from others' mistakes, systematic process improvement.

3.  **Test Documentation & Organization**
    *   Documentation Standards (*e.g., IEEE*): Define artifacts like Test Plans, Test Case Specifications, Test Incident Reports (Issue Reports), and Test Summary Reports.
    *   Key Practical Documents: Test Case Specifications (often as executable test scripts) and Issue Reports (detailing failures for reproduction).
    *   **Test Organization Models**:
        *   Developers test their own code: Common in small teams, but prone to "blind spots."
        *   Developers test each other's code: Peer review, improves quality but requires cross-knowledge.
        *   Dedicated Testers within Teams: Specialized testers embedded with developers.
        *   Independent Test Team/Group: Separate organizational unit for testing, potentially leading to "us vs. them" conflicts.
        *   Central QA Group: High-level organizational oversight.
        *   Outsourced Testing: Third-party companies provide testing as a service.
        *   Crowdsourced Testing: Leveraging a large, diverse external pool of testers.
    *   Qualities of a Good Tester: Analytical skills, technical skills (programming knowledge), communication skills, ability to provide constructive feedback, resilience to frustration.

4.  **Test Process Improvement & Maturity Models**
    *   Goal: Continuously improve the quality assurance process.
    *   Approach: Analyze defects found, identify root causes, and implement corrective actions.
    *   **Maturity Models** (*e.g., TMM, CMM*): Assess an organization's maturity in its testing/software development processes on a scale (typically 1 to 5).
        *   Level 1 (Initial): Chaotic, ad-hoc.
        *   Level 2 (Managed): Basic processes are in place and followed.
        *   Level 3 (Defined): Standardized, documented processes across the organization.
        *   Level 4 (Quantitatively Managed): Processes are measured, analyzed, and controlled statistically.
        *   Level 5 (Optimizing): Continuous process improvement based on feedback and quantitative analysis.

5.  **Exam Preparation Guide**
    *   Format: Open book, open laptop, physical presence required. No human communication allowed.
    *   Duration: 100 minutes.
    *   Structure:
        *   Part 1 (22 points): Multiple-choice questions (similar to quizzes, covering all topics).
        *   Part 2 (8 points): Two open-ended tasks requiring written answers, small calculations, or pseudo-code snippets.
    *   Content Covered (Everything except self-study/skipped sections):
        *   Lecture 1: Vocabulary (error, fault, failure, test case, test levels), quality, validation vs. verification.
        *   Black Box Testing: Equivalence Class Partitioning, Boundary Value Analysis, Combinatorial Testing, Metamorphic Testing, Exploratory Testing.
        *   White Box Testing: Control Flow Coverage (Statement, Branch, MCDC, Independent Paths), Data Flow Testing (Defs, Uses, DU Paths), Mutation Testing.
        *   Static Analysis: Static Code Analysis tools (`SpotBugs`), Symbolic Execution.
        *   Agile Testing & Automation: Test-Driven Development, Behavior-Driven Development (`Cucumber`, `Gherkin`), Test Automation (`Selenium`, `Randoop`, `EvoSuite`, GUI tools).
        *   Specialized Topics: Security Testing basics, Usability Testing basics, A/B Testing.
        *   Quality Estimation: Capture-Recapture model.
    *   Key for Part 2:
        *   Be able to draw/interpret Control Flow Graphs.
        *   Analyze code snippets for coverage (statement, branch, data flow, mutation).
        *   Perform calculations (*e.g., capture-recapture, cyclomatic complexity*).
        *   Explain reasoning clearly and concisely.
        *   Potentially write small test snippets (pseudo-code or actual code) to demonstrate coverage.
    *   Strategy: Read questions calmly, manage time, ensure answers directly address the question, clearly label sub-answers.