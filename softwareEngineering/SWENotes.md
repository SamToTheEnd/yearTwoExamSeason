# CS2800 Software Engineering Exam Preparation Guide

## Question 1: Comparing Software Engineering Concepts

This section will cover the paired concepts that might appear in Question 1, worth about 40% of the exam. For each pair, I'll provide a brief description of each concept (4-6 lines) and explain how they're connected.

### 1. Literate Programming and Programming Standards

**Literate Programming**: Where programs are written in clear language with embedded code fragments. It emphasises readability and documentation, east for human readers rather than just instructions for machines. The code and documentation are tightly integrated, making the program's purpose and implementation clear to people who didn't write the code.

**Programming Standards**: Formalised guidelines and conventions for writing code within an organisation or project. These include rules for naming conventions, formatting, commenting, and code organisation. Standards ensure consistency across a codebase, making it easier to read, maintain, and debug by developers who didn't write the original code.

**Connection**: Both literate programming and programming standards aim to improve code readability and maintainability but through different approaches. Literate programming focuses on extensive narrative documentation integrated with code, while standards create consistency through prescribed rules. Standards often include requirements for documentation, though typically less extensive than literate programming advocates. 

### 2. UML Class Diagram and Design Patterns

**UML Class Diagram**: A  diagram in the Unified Modeling Language that shows the system's classes, their attributes, operations, and relationships between classes. It provides a view of the application's structure, helping visualise object-oriented systems before implementation.

**Design Patterns**: Reusable solutions to common problems in software design. These patterns represent very good practices evolved over time by experienced developers. They provide templates for how to solve problems that can be used in many different situations, making software development more efficient and the resulting code more maintainable.

**Connection**: UML class diagrams are often used to document and communicate design patterns. Each design pattern has a characteristic structure that can be visualised as a class diagram, making it easier to understand and implement.  Design patterns are often taught and communicated using UML class diagrams as their visual representation.

### 3. Too Many Comments Smell and Too Few Comments Smell

**Too Many Comments Smell**: A code smell where excessive commenting obscures the code itself. This often indicates that the code is unclear and requires explanation rather than being self-explanatory. It can lead to maintenance issues when comments become outdated while code changes, resulting in misleading documentation that contradicts the actual behavior.

**Too Few Comments Smell**: A code smell where insufficient comments make code difficult to understand, particularly for complex algorithms or business rules. When critical reasoning or non-obvious decisions lack explanation, future developers must reverse-engineer the code's intent, increasing maintenance costs and the risk of introducing bugs during modifications.

**Connection**: Both code smells represent imbalances in the relationship between code and documentation. The ideal is clean, self-documenting code with strategic comments that explain "why" rather than "what" when necessary. These smells indicate opposite failures in achieving that balance - either compensating for unclear code with excessive explanation or failing to provide necessary context for complex logic. Good software engineering practice avoids both extremes by writing clear code that needs minimal but strategic commenting.

### 4. Reintegration Merge and Sync Merge

**Reintegration Merge**: A version control operation where changes from a feature branch are merged back into the main development branch, typically after the feature is complete. This operation completes the feature development lifecycle by incorporating the completed work into the shared codebase, making it available to all developers and for future releases.

**Sync Merge**: A version control operation where changes from the main development branch are merged into a feature branch to keep the feature branch updated with ongoing development. This prevents the feature branch from becoming too divergent from the main codebase.

**Connection**: Both operations manage the flow of changes between branches in version control systems but serve complementary purposes in the feature branch workflow. Sync merges bring parent branch changes into feature branches to keep them current, while reintegration merges push completed feature changes back to the parent branch. Together, they form a complete cycle for feature development: create branch, develop with periodic sync merges, and finally perform reintegration merge. This workflow helps teams collaborate while isolating incomplete work from the main codebase.

### 5. Aggregation Relationship and Composition Relationship

**Aggregation Relationship**: A form of association in object-oriented design representing a "has-a" relationship where one class (the whole) contains references to other classes (the parts). In aggregation, the lifetime of parts is independent of the whole—parts can exist before the whole is created and continue to exist after it's destroyed. It's represented in UML with an empty diamond on the "whole" side.

**Composition Relationship**: A stronger form of aggregation representing a "contains-a" relationship where the whole has exclusive ownership of its parts. In composition, the lifetime of parts is dependent on the whole—when the whole is destroyed, its parts are destroyed as well. Parts cannot belong to multiple wholes simultaneously. 

**Connection**: Both aggregation and composition are ways to model "whole-part" relationships in object-oriented systems, but they differ in the strength of coupling between objects. They represent different levels of object ownership and lifecycle dependency, with composition indicating stronger coupling than aggregation. Choosing between them involves considering how objects should be created, shared, and destroyed. Both relationships help developers design more maintainable systems by explicitly modeling object dependencies and lifecycle management.

### 6. Software Testing Levels and Test Driven Development

**Software Testing Levels**:
- **Unit Testing**: Testing individual components or functions in isolation, typically automated and written by developers. Unit tests verify that each part of the code works correctly on its own.
- **Integration Testing**: Testing how components work together, focusing on the interactions between integrated units. These tests verify that different parts of the system cooperate correctly.
- **System Testing**: Testing the complete, integrated system to verify it meets specified requirements. System tests evaluate the application as a whole from end-to-end.

**Test Driven Development (TDD)**: A software development approach where tests are written before the implementation code. The process follows a red-green-refactor cycle: write a failing test (red), implement the minimal code needed to pass the test (green), then refactor to improve code quality while ensuring tests still pass. TDD ensures code is testable by design and that all code has associated tests.

**Connection**: TDD is a methodology that influences how and when tests at different levels are written. While TDD typically focuses on unit tests, its principles can be applied at integration and system levels too. By writing tests first, developers clarify requirements and design interfaces before implementation. This produces more testable code and comprehensive test suites across all testing levels. The different testing levels complement each other in a TDD approach: unit tests provide fast feedback during development, while integration and system tests verify that components work correctly together in the larger context.

### 7. Code Release and Incremental Business Value

**Code Release**: The process of making a specific version of software available to users. This involves packaging code, documenting changes, versioning, deployment to production environments, and potentially migration steps. Releases represent stable points in development where features and fixes are deemed ready for use in production.

**Incremental Business Value**: The concept of delivering useful functionality to stakeholders in small, frequent increments rather than waiting for a complete solution. Each increment should provide tangible benefits to users or the business, allowing for early return on investment and continuous feedback that guides further development.

**Connection**: Modern release strategies are designed around delivering incremental business value. Rather than infrequent, large releases that bundle many changes, teams aim for smaller, more frequent releases where each adds specific value to users. This approach reduces risk, accelerates feedback cycles, and allows businesses to realize returns sooner. Continuous Integration/Continuous Deployment (CI/CD) practices enable this connection by making releases more automated and reliable, removing technical barriers to frequent delivery of incremental value.

### 8. Centralised Version Control Systems and Distributed Version Control Systems

**Centralised Version Control Systems (CVCS)**: A version control paradigm where a single central repository stores all versioned files and change history. Developers check out files from this central location, make changes, and commit back to it. Examples include Subversion (SVN) and CVS. CVCS requires network access to the central server for most operations and provides a single source of truth for project history.

**Distributed Version Control Systems (DVCS)**: A version control paradigm where each developer has a complete local copy of the repository, including its full history. Developers can work, commit, branch, and merge locally without network access, then synchronize changes with other repositories when needed. Examples include Git and Mercurial. DVCS offers greater flexibility for offline work and experimental branches.

**Connection**: Both systems aim to track changes to software over time and facilitate collaboration, but they represent fundamentally different approaches to managing code history. CVCS follows a client-server model with centralized authority, while DVCS uses a peer-to-peer model where each copy is essentially equal. The shift from CVCS to DVCS reflects broader trends in software development toward greater flexibility, offline capability, and distributed teams. Many modern workflows combine elements of both, using DVCS tools like Git with centralized workflows around main repositories hosted on services like GitHub.

### 9. Dependency Injection (DI) and Inversion of Control (IoC)

**Dependency Injection (DI)**: A design pattern where objects receive their dependencies from external sources rather than creating them internally. This approach removes hard-coded dependencies and makes the system more modular and testable. Dependencies can be injected through constructors, setters, or interfaces, allowing for different implementations to be substituted without changing the dependent class.

**Inversion of Control (IoC)**: A broader programming principle where control flow is inverted compared to traditional programming. Instead of the application code controlling the flow and calling framework methods, the framework controls the flow and calls application code. This inversion allows for more flexible designs where behavior can be changed without modifying the framework.

**Connection**: Dependency Injection is a specific technique for implementing Inversion of Control. IoC is the general principle that a class should not create its dependencies but rather receive them from outside, while DI is the concrete mechanism for providing those dependencies. Frameworks like Spring implement IoC containers that manage dependency injection, creating and injecting objects as needed. Together, they promote loose coupling, testability, and modularity by separating object creation and usage concerns.

### 10. Agile Manifesto and Software Development Models

**Agile Manifesto**: A set of values and principles for software development that emphasizes individuals and interactions, working software, customer collaboration, and responding to change. The manifesto was created in 2001 by 17 software developers seeking alternatives to documentation-driven, heavyweight development processes.

**Software Development Models** (Waterfall, Spiral, SCRUM): Different approaches to organizing the software development process. The Waterfall model is linear and sequential, proceeding through phases without returning to previous ones. The Spiral model combines iterative development with systematic risk management. The SCRUM model is an agile framework focused on delivering value in short iterations called sprints.

**Connection**: The Agile Manifesto represents a shift away from traditional models like Waterfall toward more flexible approaches like SCRUM. While Waterfall approaches software development as a single, comprehensive project with distinct phases, agile methods break development into smaller increments with minimal planning, directly reflecting the Agile Manifesto's value of "responding to change over following a plan."

### 11. Build Automation Tools and Maven Lifecycle

**Build Automation Tools**: Software tools that automate the process of compiling source code, packaging binaries, running tests, and deploying applications. They streamline the build process, ensure consistency, and reduce manual errors. Examples include Maven, Gradle, and Ant.

**Maven Build Lifecycle Phases**: Standardized stages in the Maven build process, including:
- validate: Validates project structure
- compile: Compiles source code
- test: Runs unit tests
- package: Packages compiled code (e.g., into JAR)
- verify: Runs integration tests
- install: Installs package into local repository
- deploy: Copies package to remote repository

**Dependencies**: External libraries or modules that a software project requires to function correctly. Build tools like Maven manage dependencies by downloading them from repositories and including them in the build process.

**Connection**: Build automation tools like Maven provide a standardized approach to building and deploying software projects through well-defined lifecycle phases. By automating these processes, teams ensure consistency across different environments and reduce the "it works on my machine" problem. The dependency management feature allows developers to declare what libraries they need without manually downloading and including them. Together, these capabilities significantly improve productivity and code maintainability by standardizing build processes across teams and projects.

### 12. Integrated Development Environment (IDE) and Coding Standards

**Integrated Development Environment (IDE)**: A software application that provides comprehensive facilities for software development, typically including a code editor, build automation tools, debugger, syntax highlighting, code completion, and version control integration. Examples include IntelliJ IDEA, Eclipse, and Visual Studio Code.

**Coding Standards**: Formalized guidelines and conventions for writing code within an organization or project. These include rules for naming conventions, formatting, commenting, and code organization. Standards ensure consistency across a codebase, making it easier to read, maintain, and debug by developers who didn't write the original code.

**Connection**: IDEs often incorporate tools that enforce coding standards through formatters, linters, and static analysis plugins. They provide immediate feedback on standard violations while coding, rather than discovering issues later in the development process. Modern IDEs can automatically format code according to specified standards and highlight deviations, making it easier for developers to adhere to team conventions without memorizing all rules. Together, IDEs and coding standards create an environment that promotes code quality and consistency from the moment code is written.


### 13. Javadoc and Static Analysis

**Javadoc**: A documentation generation tool for Java that extracts specially formatted comments from source code and generates HTML documentation. These comments describe classes, methods, and fields using specific tags like `@param`, `@return`, and `@throws`. Javadoc helps developers understand how to use code without having to read the implementation.

**Static Analysis**: The process of examining code without executing it to find potential issues, enforce coding standards, and improve quality. Static analysis tools can detect bugs, security vulnerabilities, performance issues, and maintainability problems early in development. Popular Java static analysis tools include:
- **Checkstyle**: Enforces coding standards and style conventions
- **SpotBugs**: Identifies potential bugs and questionable practices

**Connection**: Both Javadoc and static analysis tools contribute to code quality but address different aspects. Javadoc focuses on documenting code interfaces for human readers, while static analysis examines the code itself for potential issues. Together, they form part of a comprehensive quality assurance strategy. Modern IDEs integrate both, highlighting missing or incorrect Javadoc and flagging static analysis warnings as code is written. This integration helps developers address documentation and code quality simultaneously during development rather than as separate activities.


### 14. Continuous Integration (CI) and Continuous Deployment (CD)

**Continuous Integration (CI)**: A development practice where developers frequently integrate their code changes into a shared repository, typically multiple times per day. Each integration triggers automated builds and tests to detect integration errors quickly. CI aims to reduce integration problems and improve software quality by providing immediate feedback on code changes.

**Continuous Deployment (CD)**: An extension of CI where code changes that pass all automated tests are automatically deployed to production or staging environments without manual intervention. CD aims to make software releases more reliable and frequent by automating the deployment process and eliminating error-prone manual steps.

**Connection**: CI and CD form a pipeline that automates the software delivery process from code changes to production deployment. CI focuses on quickly validating that new changes integrate well with existing code, while CD extends this automation to the delivery process. Together, they enable teams to deliver small, incremental changes frequently and reliably. This approach reduces risk by making smaller, more manageable changes and catching issues early when they're easier to fix. The CI/CD pipeline is fundamental to modern agile and DevOps practices, allowing teams to respond quickly to changing requirements and user feedback.


### 15. Clean Code and Technical Debt

**Clean Code**: Code that is easy to read, understand, and modify. Characteristics include meaningful names, small functions with a single purpose, minimal duplication, clear organization, and comprehensive tests. Clean code prioritizes readability and maintainability over cleverness or performance optimizations that obscure intent.

**Technical Debt**: A metaphor comparing suboptimal code to financial debt. It represents the extra development work that arises when code that is easy to implement in the short run is used instead of applying the best overall solution. Like financial debt, technical debt incurs "interest" in the form of extra effort required for future development if not addressed.

**Connection**: Clean code and technical debt represent opposite ends of a spectrum in code quality. Clean code practices reduce technical debt by creating maintainable, understandable systems, while accumulated technical debt makes code increasingly difficult to maintain. Regular refactoring converts "debt-laden" code into cleaner code, essentially "paying down" the technical debt. Organizations must balance the short-term expedience that creates technical debt against the long-term costs of maintaining suboptimal code. Sustainable development requires managing this balance through regular refactoring and maintaining quality standards.

**Issue Tracking System**: A software application that manages and maintains lists of issues or tasks needed for a project. These systems track bugs, feature requests, tasks, and other work items through their lifecycle from creation to resolution. Examples include Jira, GitHub Issues, and Trello. Issue tracking systems provide visibility into project progress and help teams prioritize work.

**Code Review**: The systematic examination of code by peers to identify bugs, improve code quality, and ensure adherence to standards. Code reviews can be:
- **Code Inspection**: A formal, structured review process with defined roles and checklists
- **Modern Code Review**: A lightweight, tool-assisted process often integrated with version control (e.g., pull requests in GitHub)

**Best Practices** for code reviews include focusing on code, not the developer; setting clear expectations; reviewing manageable chunks; and providing constructive feedback.

**Connection**: Issue tracking systems and code reviews are complementary practices in software quality management. Issues documented in tracking systems often trigger development work that ultimately undergoes code review before completion. Modern tools integrate these workflows—for example, GitHub connects issues directly to pull requests, which serve as the venue for code review. This integration creates traceability from the initial problem or feature request through development and review to final implementation. Together, they ensure that work is properly tracked, prioritized, and quality-checked before being merged into the codebase.

### 16. Single Responsibility Principle (SRP) and Separation of Concerns

**Single Responsibility Principle (SRP)**: One of the SOLID principles stating that a class should have only one reason to change, meaning it should have only one responsibility or job. This principle encourages creating classes that are focused on a single aspect of the system, making them easier to understand, test, and maintain. When requirements change, only classes directly related to that change need modification.

**Separation of Concerns**: A design principle for separating a program into distinct sections, each addressing a separate concern or aspect of functionality. Examples include separating business logic from presentation logic or data access code. This separation makes systems more maintainable by localizing changes and allowing different concerns to evolve independently.

**Connection**: The Single Responsibility Principle can be seen as applying Separation of Concerns at the class level. Both principles aim to create more maintainable software by breaking down complex systems into smaller, more focused parts. SRP provides specific guidance for class design within the broader philosophy of Separation of Concerns. Together, they help developers create systems where functionality is logically organized, changes are localized, and different aspects can be understood, developed, and maintained independently.

### 17. Design Principles: No Silver Bullet and Separation of Concerns

**No Silver Bullet**: A principle from Fred Brooks' essay arguing that there is no single development approach, technology, or practice that will dramatically improve software productivity by an order of magnitude. Software development's essential complexity cannot be eliminated because it comes from the problem domain itself. This principle cautions against expecting miracle solutions to inherently complex problems.

**Separation of Concerns**: A design principle for separating a program into distinct sections, each addressing a separate concern or aspect of functionality. Examples include separating business logic from presentation logic or data access code. This separation makes systems more maintainable by localizing changes and allowing different concerns to evolve independently.

**Connection**: Both principles address fundamental aspects of managing software complexity. No Silver Bullet recognizes the inherent complexity in software development that cannot be eliminated, while Separation of Concerns provides a strategy for managing that complexity by dividing it into smaller, more focused pieces. Separation of Concerns doesn't eliminate the essential complexity that No Silver Bullet warns about, but it makes that complexity more manageable by organizing the system logically. Together, these principles encourage realistic expectations about software development challenges while providing practical approaches to architectural design.


### 18. UML Sequence and Activity Diagrams

**Sequence Diagram**: A UML behavioral diagram that shows object interactions arranged in time sequence. It depicts the objects involved in the scenario and the sequence of messages exchanged between them to carry out functionality. Sequence diagrams are excellent for visualizing the runtime behavior of a system, showing how objects collaborate and the order of operations.

**Activity Diagram**: A UML behavioral diagram representing workflows of stepwise activities and actions, with support for choice, iteration, and concurrency. Activity diagrams are useful for modeling business processes, workflows, and algorithmic logic. They focus on the flow of control from activity to activity rather than messages between objects.

**Connection**: Both sequence and activity diagrams visualize dynamic aspects of software systems but emphasize different perspectives. Sequence diagrams focus on object interactions and message passing, making them ideal for detailed design of method calls between classes. Activity diagrams capture higher-level processes and workflows, showing decision points and parallel activities. Together, they provide complementary views of system behavior—sequence diagrams show "how" objects interact to accomplish a task, while activity diagrams show "what" happens during a process, regardless of which objects are involved.

###  Design Principles: DRY, KISS, and YAGNI

**DRY (Don't Repeat Yourself)**: A principle that states every piece of knowledge or logic should have a single, unambiguous representation within a system. It aims to reduce duplication by abstracting common elements into reusable components, making maintenance easier and reducing inconsistencies.

**KISS (Keep It Simple, Stupid!)**: A design principle advocating simplicity as a key goal. Solutions should be as simple as possible (but no simpler) to minimize complexity and make code easier to understand and maintain. KISS discourages unnecessary complexity that doesn't add value.

**YAGNI (You Aren't Gonna Need It)**: A principle encouraging developers to implement features only when actually needed, not when they anticipate needing them. YAGNI advises against adding functionality based on speculation about future requirements, as this often leads to unused code and unnecessary complexity.

### SOLID Principles: A set of five design principles for writing maintainable and extensible object-oriented code:

- **Single Responsibility Principle (SRP)**: A class should have only one reason to change, meaning it should have only one responsibility or job.
- **Open-Closed Principle (OCP)**: Software entities should be open for extension but closed for modification, allowing behavior changes through inheritance or interfaces without altering existing code.
- **Liskov Substitution Principle (LSP)**: Objects of a superclass should be replaceable with objects of subclasses without affecting program correctness.
- **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they don't use, favoring multiple specific interfaces over a single general-purpose one.
- **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

## Question 2: Code Analysis, Standards, and Code Smells

This section focuses on code analysis, programming standards, code smells, control flow, cyclomatic complexity, and testing concepts.

### Programming Standards

Programming standards are formalized guidelines and conventions for writing code within an organization or project. They include:

1. **Naming conventions**:
  - Classes use PascalCase (e.g., `CustomerService`)
  - Methods and variables use camelCase (e.g., `calculateTotal`)
  - Constants use UPPER_SNAKE_CASE (e.g., `MAX_RETRY_COUNT`)

2. **Formatting rules**:
  - Indentation (spaces vs. tabs, amount)
  - Brace placement (same line or next line)
  - Maximum line length
  - Spacing around operators

3. **Documentation requirements**:
  - Javadoc for public methods and classes
  - Comment styles and coverage

#### Why Automatic Checking Is Important

Programming standards should be automatically checkable because:

1. Manual checking is time-consuming and error-prone
2. Automated tools provide consistent enforcement
3. They can be integrated into CI/CD pipelines for continuous verification
4. Developers get immediate feedback during development
5. They reduce subjective disagreements in code reviews

#### Common Java Standards for Variable Naming

1. **camelCase for variables and methods**: Variables and method names start with lowercase letter and use camelCase (e.g., `customerName`, `calculateTotal`).

2. **No Hungarian notation**: Variable names should not include type information as prefixes (e.g., use `count` instead of `iCount`).

3. **Descriptive names**: Names should clearly indicate purpose (e.g., `numberOfStudents` rather than `n`).

4. **Constants in UPPER_SNAKE_CASE**: Constants should be all uppercase with underscores (e.g., `MAX_RETRY_COUNT`).

### Code Smells

Code smells are indicators of potential problems in code that may require refactoring.

#### Too Few Comments Smell

**Definition**: Code lacks necessary explanations for complex logic, business rules, or non-obvious decisions.

**Why it matters**:
- Future developers cannot understand the reasoning behind implementation choices
- Maintenance becomes difficult without context
- Bug fixes and enhancements take longer as developers must reverse-engineer intent
- Knowledge is lost when original developers leave

**What it indicates about the engineer**:
- They may prioritize writing code over documentation
- They might assume their code is self-explanatory when it isn't
- They could be working under time pressure, cutting corners on documentation
- They may not consider the needs of future maintainers

#### Dead Code Smell

**Definition**: Code that is never executed or used but remains in the codebase (commented-out code, unreachable conditions, unused variables or methods).

**Why it matters**:
- Increases cognitive load when reading the code
- Creates confusion about what functionality is actually active
- Makes maintenance more difficult as developers must determine relevance
- Increases risk when making changes (is it safe to remove?)
- Bloats the codebase unnecessarily

**What it indicates about the engineer**:
- Uncertainty about whether code might be needed in the future
- Fear of completely removing code in case it's needed later
- Lack of trust in version control to recover removed code
- Poor discipline in cleaning up after changes
- Possible lack of understanding about what code is actually used

### Control Flow and Cyclomatic Complexity

#### Control Flow Graph (CFG)

A Control Flow Graph is a representation of all paths that might be traversed through a program during execution. It consists of:

- **Nodes**: Represent blocks of sequential code with no branching
- **Edges**: Represent possible paths between blocks
- **Entry node**: Where execution begins
- **Exit node**: Where execution terminates

For the given code:

```java
public int Foo(float value) throws NeverException {
    int years = -1;
    if (interest <= 0f || money <= 0f) {
        throw new NeverException();
    }
    if (value > 0) {
        for (years = 0; money < value; years = years + 1)
            value = value * (1.0f + interest / 100.0f);
    } else {
        years = 0;
    }
    return years;
}
```

A control flow graph would have nodes representing:
1. Method entry, initialize `years = -1`
2. Check if `interest <= 0f || money <= 0f`
3. Throw exception
4. Check if `value > 0`
5. Initialize `years = 0`
6. Check loop condition `money < value`
7. Loop body: `value = value * (1.0f + interest / 100.0f)`
8. Increment `years`
9. Set `years = 0` (else branch)
10. Return `years`

Edges would connect these nodes based on possible execution paths.

#### Cyclomatic Complexity

Cyclomatic complexity measures the number of linearly independent paths through a program's source code. It's calculated using the formula:

```
M = E - N + 2P
```

Where:
- E = number of edges in the control flow graph
- N = number of nodes in the control flow graph
- P = number of connected components (usually 1 for a single method)

Alternatively, it can be calculated as:
```
M = number of decision points + 1
```

Where decision points include:
- if statements
- while loops
- for loops
- case statements in a switch
- catch blocks
- && and || operators (each one counts separately)

For our example code, the cyclomatic complexity would be:
- 1 (base)
- +1 for `interest <= 0f || money <= 0f` condition
- +1 for the OR operator in that condition
- +1 for `value > 0` condition
- +1 for the for loop condition `money < value`
  = 5

### Unit Testing and Coverage

#### Statement Coverage

Statement coverage measures the percentage of statements in the code that are executed by tests. To achieve full statement coverage for the given code, we need tests that execute:

1. The exception path when interest or money is zero or negative
2. The path where value <= 0
3. The path where value > 0 and the loop executes at least once

Example test cases:
- Test 1: `money = 0, interest = 1, value = 10` (throws exception)
- Test 2: `money = 100, interest = 5, value = 0` (else branch, years = 0)
- Test 3: `money = 100, interest = 5, value = 200` (for loop executes)

#### Branch Coverage

Branch coverage measures the percentage of branches (decision outcomes) that are executed by tests. For full branch coverage, we need to test both outcomes of each decision point:

1. `interest <= 0f` true and false
2. `money <= 0f` true and false
3. `value > 0` true and false
4. `money < value` true and false

Example test cases:
- Test 1: `money = 0, interest = 1, value = 10` (money <= 0 is true)
- Test 2: `money = 100, interest = 0, value = 10` (interest <= 0 is true)
- Test 3: `money = 100, interest = 5, value = 0` (value > 0 is false)
- Test 4: `money = 100, interest = 5, value = 50` (money < value is false)
- Test 5: `money = 100, interest = 5, value = 200` (money < value is true initially)

## Question 3: Git and Version Control

This section covers Git concepts and operations, focusing on branches, commits, merging, and best practices.

**Git Core Concepts**:
- **Commit**: A snapshot of changes to tracked files in the repository at a specific point in time. Each commit has a unique identifier (hash) and contains metadata including the author, timestamp, and message describing the changes.
- **References**: Pointers to specific commits, including branches and tags. References make it easier to work with commits without using their hash values directly.
- **HEAD**: A special reference that points to the current commit or branch the user is working on. It represents the "current position" in the repository's history.
- **Staging Area**: An intermediate area between the working directory and repository. Changes must be added to the staging area before they can be committed, allowing selective commits of modified files.
- **Branch**: A movable pointer to a specific commit, representing an independent line of development. Branches allow parallel development without affecting the main codebase.
- **Merge**: The process of integrating changes from one branch into another. Git automatically combines changes when possible and highlights conflicts that require manual resolution.
- **Conflict**: Occurs when Git cannot automatically merge changes because the same part of a file was modified differently in the branches being merged. Conflicts must be resolved manually.
- **Tags**: Named references that point to specific commits, typically used to mark release versions. Unlike branches, tags don't move as new commits are created.
- **Remotes**: References to repositories hosted on other machines or servers, enabling collaboration. Developers can push changes to and pull changes from remote repositories.
- **.gitignore**: A file that specifies intentionally untracked files that Git should ignore, such as build outputs, dependencies, or local configuration files.

**Git Commands**:
- `git status`: Shows the current state of the working directory and staging area.
- `git add`: Adds file changes to the staging area in preparation for a commit.
- `git commit`: Creates a new commit with the changes currently in the staging area.
- `git push`: Uploads local repository commits to a remote repository.

### Git Core Concepts

#### Commit

A commit in Git is a snapshot of your repository at a specific point in time. Each commit:
- Has a unique identifier (SHA hash)
- Contains metadata (author, timestamp, message)
- References its parent commit(s)
- Preserves the state of all tracked files

Example:
```bash
git commit -m "Implement user authentication feature"
```

#### Branch

A branch in Git is a lightweight, movable pointer to a commit. Branches are used to:
- Keep track of different lines of development
- Isolate changes for specific features or fixes
- Experiment without affecting the main codebase

Branches allow parallel development and help keep different lines of work separate until they're ready to be merged.

Example:
```bash
git branch feature-login     # Create a branch
git checkout feature-login   # Switch to the branch
# Or in one command:
git checkout -b feature-login
```

#### HEAD

HEAD is a special pointer that refers to the current commit you're working on. It typically points to the tip of the current branch but can be detached to point directly to a specific commit.

Example:
```bash
git log --oneline    # Shows commits with HEAD pointing to the latest
git checkout a1b2c3  # Detaches HEAD to point to commit a1b2c3
```

#### Tags

Tags in Git are references that point to specific points in Git history. Unlike branches, tags don't move - they're attached to a specific commit permanently. They're typically used to mark release points.

Types of tags:
- Lightweight tags: Just a name for a commit
- Annotated tags: Store extra metadata (tagger name, date, message)

Example:
```bash
git tag v1.0.0                                 # Lightweight tag
git tag -a v1.0.0 -m "First stable release"    # Annotated tag
```

Difference between tags and branches:
1. **Purpose**: Tags mark specific points in history (like releases), while branches represent lines of development
2. **Movement**: Branches move with new commits, tags are fixed
3. **Lifecycle**: Branches are often temporary, tags are permanent
4. **Default checkout behavior**: Checking out a branch puts you in a state to add new commits; checking out a tag puts you in a detached HEAD state

### Git Operations

#### Merge

Merging in Git combines changes from different branches. The main types are:

1. **Fast-forward merge**: When the target branch is a direct descendant of the source branch, Git simply moves the pointer forward.

   ```bash
   # On main branch
   git merge feature     # If main hasn't changed since feature branched
   ```

2. **Three-way merge**: When both branches have diverged, Git creates a new merge commit that combines changes from both branches.

   ```bash
   # On main branch with independent commits
   git merge feature     # Creates a merge commit
   ```

#### Merge Conflicts

Conflicts occur when Git can't automatically resolve differences between branches being merged. They happen when:
- The same lines are changed in different ways on different branches
- A file is deleted on one branch but modified on another

Resolving conflicts involves:
1. Opening conflicted files and editing them to resolve differences
2. Marking conflicts as resolved with `git add`
3. Completing the merge with `git commit`

Example of a conflict marker in a file:
```
<<<<<<< HEAD
This is the change from the current branch
=======
This is the change from the branch being merged in
>>>>>>> feature-branch
```

#### Push and Pull

**git push** sends local commits to a remote repository. It's used to share your changes with others.

```bash
git push origin main     # Push main branch to origin remote
```

Reasons why it's not a good idea to immediately follow each commit with a push:
1. **Incomplete features**: Pushing partial work can break the codebase for others
2. **Untested changes**: You haven't had a chance to test changes thoroughly
3. **Multiple related commits**: You might want to squash several commits before sharing
4. **Local history rewriting**: You can't easily amend or rebase commits after pushing

**git pull** fetches changes from a remote repository and merges them into your local branch.

```bash
git pull origin main     # Get changes from origin's main and merge them
```

#### Revert

The `git revert` command creates a new commit that undoes the changes made by a previous commit. It's a safe way to undo changes as it doesn't alter history.

```bash
git revert a1b2c3     # Create a new commit that undoes commit a1b2c3
```

### Git Best Practices

#### Good Commit Messages

Commit messages should be clear, meaningful, and follow conventions:
- First line: concise summary (50 chars or less)
- Blank line
- Detailed explanation if necessary

Bad commit messages to avoid:
1. **"Fixed the Checkstyle Violations and added the missing Javadoc"**
  - Problem: Combines unrelated changes
  - Better approach: Separate into distinct commits for each concern

2. **"Successful Commit. The fault is now fixed."**
  - Problem: Doesn't describe what was fixed
  - Better approach: "Fix null pointer exception in UserService.login()"

3. **"Saving and pushing code because it is lunchtime. Will complete the test case later this afternoon."**
  - Problem: Indicates incomplete work and timing rather than content
  - Better approach: Complete the work before committing or use a local branch

#### Feature Branch Workflow

Advantages of using feature branches:
1. **Isolation**: Changes don't affect others until merged
2. **Parallel development**: Multiple features can be developed simultaneously
3. **Code review**: Changes can be reviewed as a cohesive unit before merging
4. **Experimentation**: Dead-end approaches can be abandoned without cleanup
5. **Stability**: Main branch remains stable for releases
6. **Focus**: Developers can concentrate on one feature at a time

Example workflow:
```bash
# Start a new feature
git checkout -b feature-user-profiles main

# Make changes, commit work
git add .
git commit -m "Add user profile page"

# Get latest changes from main
git checkout main
git pull
git checkout feature-user-profiles
git merge main

# Push feature branch for review
git push origin feature-user-profiles

# After review, merge to main
git checkout main
git merge feature-user-profiles
git push origin main
```

## Question 4: Design Patterns and UML

This section covers design patterns, UML diagrams, and software design principles.

### Design Patterns


**Design Patterns**: Reusable solutions to common problems in software design. These patterns represent best practices evolved over time by experienced developers. They provide templates for how to solve problems that can be used in many different situations, making software development more efficient and the resulting code more maintainable.

**Pattern Categories**:
- **Creational Patterns**: Focus on object creation mechanisms, trying to create objects in a manner suitable to the situation.
  - **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access to it.
  - **Factory Pattern**: Creates objects without exposing the instantiation logic and refers to the newly created object using a common interface.
  - **Builder Pattern**: Separates object construction from its representation, allowing the same construction process to create different representations.
- **Behavioral Patterns**: Identify common communication patterns between objects and realize these patterns.
  - **Observer Pattern**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
  - **State Pattern**: Allows an object to alter its behavior when its internal state changes, appearing to change its class.
  - **Visitor Pattern**: Represents an operation to be performed on the elements of an object structure without changing the classes of the elements on which it operates.
- **Structural Patterns**: Ease the design by identifying a simple way to realize relationships between entities.
  - **Facade Pattern**: Provides a unified interface to a set of interfaces in a subsystem, defining a higher-level interface that makes the subsystem easier to use.
  - **Adapter Pattern**: Allows incompatible interfaces to work together by creating a middle-layer adapter that converts one interface to another.
  - **Bridge Pattern**: Decouples an abstraction from its implementation so that the two can vary independently.


# Software Engineering Design Patterns

## Factory Pattern

### Overview
The Factory pattern is a creational design pattern that provides an interface for creating objects without specifying their concrete classes. It encapsulates object creation logic, allowing a client to create objects without knowing the specific classes being instantiated.

### Key Components
- **Factory**: A class that contains a method to create and return instances of different classes based on input parameters
- **Product Interface**: A common interface implemented by all created objects
- **Concrete Products**: Specific implementations of the Product interface

### Implementation
```java
// Product interface
interface Product {
    void operation();
}

// Concrete products
class ConcreteProductA implements Product {
    @Override
    public void operation() {
        System.out.println("ConcreteProductA operation");
    }
}

class ConcreteProductB implements Product {
    @Override
    public void operation() {
        System.out.println("ConcreteProductB operation");
    }
}

// Factory
class ProductFactory {
    public Product createProduct(String productType) {
        if ("A".equals(productType)) {
            return new ConcreteProductA();
        } else if ("B".equals(productType)) {
            return new ConcreteProductB();
        }
        throw new IllegalArgumentException("Unknown product type");
    }
}
```

### Why It's Important
1. **Decoupling**: Separates product creation from the client that uses the products
2. **Centralized Creation Logic**: Centralizes complex instantiation logic
3. **Dynamic Type Selection**: Allows selection of object type at runtime
4. **Single Responsibility**: Factory handles only object creation, adhering to the Single Responsibility Principle

### Connection to Other Patterns
- **Factory vs. Singleton**: Factory creates multiple instances; it can be used to implement a Singleton by ensuring only one instance is ever returned
- **Factory Method vs. Abstract Factory**: Factory Method is a single method for creating objects, while Abstract Factory is a full class with multiple methods for creating families of related objects

## Facade Pattern

### Overview
The Facade pattern provides a simplified interface to a complex subsystem of classes. It doesn't encapsulate the subsystem but provides a higher-level interface that makes the subsystem easier to use.

### Key Components
- **Facade**: A class that provides a simple interface to a complex subsystem
- **Subsystem Classes**: The complex system of classes that the facade simplifies

### Implementation
```java
// Subsystem classes
class SubsystemA {
    public void operationA() {
        System.out.println("Subsystem A operation");
    }
}

class SubsystemB {
    public void operationB() {
        System.out.println("Subsystem B operation");
    }
}

class SubsystemC {
    public void operationC() {
        System.out.println("Subsystem C operation");
    }
}

// Facade
class Facade {
    private SubsystemA subsystemA;
    private SubsystemB subsystemB;
    private SubsystemC subsystemC;
    
    public Facade() {
        this.subsystemA = new SubsystemA();
        this.subsystemB = new SubsystemB();
        this.subsystemC = new SubsystemC();
    }
    
    // Simplified interface method
    public void operation() {
        subsystemA.operationA();
        subsystemB.operationB();
        subsystemC.operationC();
    }
}
```

### Why It's Important
1. **Simplification**: Provides a simple entry point to a complex system
2. **Decoupling**: Shields clients from subsystem components, reducing dependencies
3. **Layering**: Creates a separation between layers in an application
4. **Higher-level Interface**: Offers a higher-level interface that's easier to understand and use

### Connection to Other Patterns
- **Facade vs. Adapter**: Both wrap existing classes, but a Facade simplifies a complex subsystem, while an Adapter makes incompatible interfaces compatible
- **Facade vs. Mediator**: Facade provides a simplified interface to subsystems, whereas Mediator coordinates interactions between objects

## Builder Pattern

### Overview
The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It's particularly useful when creating objects with many optional parameters.

### Key Components
- **Builder Interface**: Specifies methods for creating the parts of a product
- **Concrete Builder**: Implements the Builder interface to create and assemble parts of the product
- **Director**: Constructs the object using the Builder interface (optional)
- **Product**: The complex object being built

### Implementation
```java
// Product
class House {
    private String foundation;
    private String structure;
    private String roof;
    private boolean hasGarage;
    private boolean hasSwimmingPool;
    
    // Getters
    public String getFoundation() { return foundation; }
    public String getStructure() { return structure; }
    public String getRoof() { return roof; }
    public boolean hasGarage() { return hasGarage; }
    public boolean hasSwimmingPool() { return hasSwimmingPool; }
    
    // Setters
    public void setFoundation(String foundation) { this.foundation = foundation; }
    public void setStructure(String structure) { this.structure = structure; }
    public void setRoof(String roof) { this.roof = roof; }
    public void setGarage(boolean hasGarage) { this.hasGarage = hasGarage; }
    public void setSwimmingPool(boolean hasSwimmingPool) { this.hasSwimmingPool = hasSwimmingPool; }
}

// Builder interface
interface HouseBuilder {
    HouseBuilder buildFoundation();
    HouseBuilder buildStructure();
    HouseBuilder buildRoof();
    HouseBuilder buildGarage();
    HouseBuilder buildSwimmingPool();
    House getResult();
}

// Concrete builder
class ModernHouseBuilder implements HouseBuilder {
    private House house;
    
    public ModernHouseBuilder() {
        this.house = new House();
    }
    
    @Override
    public HouseBuilder buildFoundation() {
        house.setFoundation("Modern Foundation");
        return this;
    }
    
    @Override
    public HouseBuilder buildStructure() {
        house.setStructure("Modern Structure");
        return this;
    }
    
    @Override
    public HouseBuilder buildRoof() {
        house.setRoof("Modern Roof");
        return this;
    }
    
    @Override
    public HouseBuilder buildGarage() {
        house.setGarage(true);
        return this;
    }
    
    @Override
    public HouseBuilder buildSwimmingPool() {
        house.setSwimmingPool(true);
        return this;
    }
    
    @Override
    public House getResult() {
        return house;
    }
}

// Director (optional)
class HouseDirector {
    public House constructBasicHouse(HouseBuilder builder) {
        return builder
            .buildFoundation()
            .buildStructure()
            .buildRoof()
            .getResult();
    }
    
    public House constructLuxuryHouse(HouseBuilder builder) {
        return builder
            .buildFoundation()
            .buildStructure()
            .buildRoof()
            .buildGarage()
            .buildSwimmingPool()
            .getResult();
    }
}
```

### Why It's Important
1. **Complex Object Creation**: Simplifies the creation of complex objects
2. **Step-by-Step Construction**: Allows construction of objects step-by-step
3. **Variable Representation**: The same construction process can create different representations
4. **Immutability**: Can be used to create immutable objects with many optional parameters
5. **Fluent Interface**: Often implements a fluent interface (method chaining)

### Connection to Other Patterns
- **Builder vs. Factory**: Factory creates objects in a single step, while Builder constructs complex objects step by step
- **Builder vs. Abstract Factory**: Abstract Factory creates families of related objects, while Builder focuses on constructing a complex object

## Observer Pattern

### Overview
The Observer pattern defines a one-to-many dependency between objects, so that when one object (the subject) changes state, all its dependents (observers) are notified and updated automatically. It's a key pattern for implementing distributed event handling systems.

### Key Components
- **Subject Interface**: Defines methods for attaching, detaching, and notifying observers
- **Concrete Subject**: Implements the Subject interface, maintains state, and notifies observers of changes
- **Observer Interface**: Defines an update method that gets called when the subject changes
- **Concrete Observer**: Implements the Observer interface, typically storing a reference to the subject

### Implementation
```java
import java.util.ArrayList;
import java.util.List;

// Observer interface
interface Observer {
    void update();
}

// Subject interface
interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

// Concrete Subject
class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private int state;
    
    public int getState() {
        return state;
    }
    
    public void setState(int state) {
        this.state = state;
        notifyObservers();
    }
    
    @Override
    public void attach(Observer observer) {
        observers.add(observer);
    }
    
    @Override
    public void detach(Observer observer) {
        observers.remove(observer);
    }
    
    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }
}

// Concrete Observer
class ConcreteObserver implements Observer {
    private ConcreteSubject subject;
    
    public ConcreteObserver(ConcreteSubject subject) {
        this.subject = subject;
        subject.attach(this);
    }
    
    @Override
    public void update() {
        System.out.println("Observer updated, new state: " + subject.getState());
    }
}
```

### Why It's Important
1. **Loose Coupling**: Subjects and observers are loosely coupled, can vary independently
2. **Event Handling**: Provides a framework for event handling systems
3. **Broadcast Communication**: Enables broadcast communication to multiple interested objects
4. **Open/Closed Principle**: You can add new observers without modifying the subject

### Connection to Other Patterns
- **Observer vs. Mediator**: Observer distributes communication by introducing Subject and Observer objects, while Mediator centralizes communication between objects
- **Observer vs. Command**: Command pattern can use Observer to implement callbacks

## Singleton Pattern

### Overview
The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across the system.

### Implementation
```java
public final class Singleton {
    // Private static instance - eager initialization
    private static final Singleton INSTANCE = new Singleton();
    
    // Private constructor prevents instantiation from other classes
    private Singleton() {
        // Prevent reflection instantiation
        if (INSTANCE != null) {
            throw new IllegalStateException("Already initialized");
        }
    }
    
    // Public static method to get the instance
    public static Singleton getInstance() {
        return INSTANCE;
    }
    
    // Business method
    public void doSomething() {
        System.out.println("Singleton is doing something");
    }
    
    // Protect against serialization
    protected Object readResolve() {
        return INSTANCE;
    }
}
```

### Lazy Initialization (Thread-Safe)
```java
public final class LazySingleton {
    private static volatile LazySingleton instance;
    
    private LazySingleton() {
        // Prevent reflection instantiation
        if (instance != null) {
            throw new IllegalStateException("Already initialized");
        }
    }
    
    public static LazySingleton getInstance() {
        if (instance == null) {
            synchronized (LazySingleton.class) {
                if (instance == null) {
                    instance = new LazySingleton();
                }
            }
        }
        return instance;
    }
}
```

### Enum Singleton (Java)
```java
public enum EnumSingleton {
    INSTANCE;
    
    public void doSomething() {
        System.out.println("Singleton is doing something");
    }
}
```

### Why It's Important
1. **Single Instance**: Ensures that a class has only one instance
2. **Global Access**: Provides a global point of access to that instance
3. **Lazy Initialization**: Can implement lazy initialization (create on first use)
4. **Thread Safety**: Can be implemented in a thread-safe way

### Connection to Other Patterns
- **Singleton vs. Factory**: Factory creates multiple different objects, while Singleton creates exactly one instance
- **Singleton vs. Static Class**: Singleton can implement interfaces, be extended (if not final), and can be lazy-loaded

### Why Not to Extend Singleton
1. **Breaks Uniqueness**: If a subclass can be instantiated, the "only one instance" guarantee is broken
2. **State Confusion**: The parent and child classes might have conflicting or confusing state
3. **Violates Purpose**: Extends against the very purpose of the Singleton pattern

### Preventing Inheritance in Java
1. Declare the class as `final`
2. Make the constructor throw an exception if an instance already exists
3. Use an enum (Java's preferred way for implementing Singletons)

## State Pattern

### Overview
The State pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class. It's a way to implement state-dependent behavior without massive conditional statements.

### Key Components
- **Context**: Maintains an instance of a ConcreteState subclass that defines the current state
- **State Interface**: Defines an interface for encapsulating state-specific behavior
- **Concrete States**: Implement behavior associated with a state of the Context

### Implementation
```java
// State interface
interface State {
    void handle(Context context);
}

// Concrete states
class ConcreteStateA implements State {
    @Override
    public void handle(Context context) {
        System.out.println("Handling in State A");
        context.setState(new ConcreteStateB());
    }
}

class ConcreteStateB implements State {
    @Override
    public void handle(Context context) {
        System.out.println("Handling in State B");
        context.setState(new ConcreteStateA());
    }
}

// Context
class Context {
    private State state;
    
    public Context() {
        // Default state
        state = new ConcreteStateA();
    }
    
    public void setState(State state) {
        this.state = state;
    }
    
    public void request() {
        state.handle(this);
    }
}
```

### Why It's Important
1. **State-Specific Behavior**: Localizes state-specific behavior in separate classes
2. **Eliminates Conditionals**: Replaces large conditional statements with polymorphism
3. **State Transitions**: Makes state transitions explicit
4. **Single Responsibility**: Each state class handles only behaviors related to that state

### Connection to Other Patterns
- **State vs. Strategy**: Both patterns use composition to change behavior, but State focuses on changing behavior based on internal state, while Strategy allows choosing algorithms at runtime
- **State vs. Command**: State encapsulates state-based behavior, while Command encapsulates a request as an object

## Bridge Pattern

### Overview
The Bridge pattern decouples an abstraction from its implementation so that the two can vary independently. It involves an interface acting as a bridge between the abstraction and its implementation.

### Key Components
- **Abstraction**: Defines the abstraction's interface and maintains a reference to the Implementor
- **Refined Abstraction**: Extends the interface defined by Abstraction
- **Implementor**: Defines the interface for implementation classes
- **Concrete Implementor**: Implements the Implementor interface

### Implementation
```java
// Implementor interface
interface DrawingAPI {
    void drawCircle(float x, float y, float radius);
}

// Concrete Implementors
class DrawingAPI1 implements DrawingAPI {
    @Override
    public void drawCircle(float x, float y, float radius) {
        System.out.printf("API1.drawCircle(%f,%f,%f)\n", x, y, radius);
    }
}

class DrawingAPI2 implements DrawingAPI {
    @Override
    public void drawCircle(float x, float y, float radius) {
        System.out.printf("API2.drawCircle(%f,%f,%f)\n", x, y, radius);
    }
}

// Abstraction
abstract class Shape {
    protected DrawingAPI drawingAPI;
    
    protected Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }
    
    public abstract void draw();
    public abstract void resizeByPercentage(float percent);
}

// Refined Abstraction
class Circle extends Shape {
    private float x, y, radius;
    
    public Circle(float x, float y, float radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        drawingAPI.drawCircle(x, y, radius);
    }
    
    @Override
    public void resizeByPercentage(float percent) {
        radius *= (1.0 + percent/100.0);
    }
}
```

### Why It's Important
1. **Separation of Concerns**: Separates an abstraction from its implementation
2. **Independent Evolution**: Abstraction and implementation can evolve independently
3. **Platform Independence**: Can help achieve platform independence
4. **Avoids Class Explosion**: Prevents an exponential increase in class count when adding new variants

### Connection to Other Patterns
- **Bridge vs. Adapter**: Adapter makes unrelated classes work together, typically applied after design. Bridge is designed upfront to let abstraction and implementation vary independently
- **Bridge vs. Strategy**: Strategy focuses on changing algorithms, while Bridge focuses on separating an abstraction from its implementation

## Adapter Pattern

### Overview
The Adapter pattern allows objects with incompatible interfaces to collaborate. It converts the interface of a class into another interface that clients expect, enabling classes to work together that couldn't otherwise due to incompatible interfaces.

### Key Components
- **Target**: Defines the domain-specific interface that the client uses
- **Adaptee**: Defines an existing interface that needs adapting
- **Adapter**: Adapts the interface of the Adaptee to the Target interface

### Implementation (Object Adapter using composition)
```java
// Target interface
interface Target {
    void request();
}

// Adaptee (existing class with incompatible interface)
class Adaptee {
    public void specificRequest() {
        System.out.println("Specific request from Adaptee");
    }
}

// Adapter
class Adapter implements Target {
    private Adaptee adaptee;
    
    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }
    
    @Override
    public void request() {
        // Translate the Target interface to Adaptee interface
        adaptee.specificRequest();
    }
}
```

### Implementation (Class Adapter using inheritance - less common in Java)
```java
// Target interface
interface Target {
    void request();
}

// Adaptee (existing class with incompatible interface)
class Adaptee {
    public void specificRequest() {
        System.out.println("Specific request from Adaptee");
    }
}

// Class Adapter
class ClassAdapter extends Adaptee implements Target {
    @Override
    public void request() {
        specificRequest();
    }
}
```

### Why It's Important
1. **Interface Compatibility**: Makes incompatible interfaces work together
2. **Code Reuse**: Enables reuse of existing classes despite incompatible interfaces
3. **Legacy Integration**: Helps integrate legacy code with modern systems
4. **Decoupling**: Decouples client code from the adapted classes

### Connection to Other Patterns
- **Adapter vs. Facade**: Adapter changes the interface of an existing object, while Facade provides a simplified interface to a subsystem
- **Adapter vs. Decorator**: Adapter changes an object's interface, Decorator enhances an object without changing its interface

### Distinguishing Adapter from Facade in Source Code
1. **Intent**: Adapter makes two incompatible interfaces work together, while Facade provides a simplified interface to a complex subsystem
2. **Code Structure**:
  - Adapter typically wraps a single class and translates methods one-to-one
  - Facade typically wraps multiple classes and provides higher-level operations that may call multiple methods on different objects
3. **Method Signatures**:
  - Adapter method names often differ from the adaptee's method names (translation)
  - Facade method names are typically new, high-level operations not present in subsystem
4. **Knowledge of Subsystem**:
  - Client using an Adapter still knows about the Target interface
  - Client using a Facade is shielded from subsystem details

## Visitor Pattern

### Overview
The Visitor pattern represents an operation to be performed on elements of an object structure. It lets you define a new operation without changing the classes of the elements on which it operates. This pattern is particularly useful when you have a stable hierarchy of classes but frequently need to define new operations on them.

### Key Components
- **Visitor Interface**: Declares visit methods for each ConcreteElement type
- **Concrete Visitor**: Implements each visit operation
- **Element Interface**: Declares an accept operation that takes a visitor as an argument
- **Concrete Element**: Implements the accept operation
- **Object Structure**: Can enumerate its elements and may provide a high-level interface for letting the visitor visit its elements

### Implementation
```java
// Element interface
interface Element {
    void accept(Visitor visitor);
}

// Concrete Elements
class ConcreteElementA implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visitConcreteElementA(this);
    }
    
    public String operationA() {
        return "ConcreteElementA";
    }
}

class ConcreteElementB implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visitConcreteElementB(this);
    }
    
    public String operationB() {
        return "ConcreteElementB";
    }
}

// Visitor interface
interface Visitor {
    void visitConcreteElementA(ConcreteElementA element);
    void visitConcreteElementB(ConcreteElementB element);
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    @Override
    public void visitConcreteElementA(ConcreteElementA element) {
        System.out.println("Visitor is processing " + element.operationA());
    }
    
    @Override
    public void visitConcreteElementB(ConcreteElementB element) {
        System.out.println("Visitor is processing " + element.operationB());
    }
}

// Object Structure
class ObjectStructure {
    private List<Element> elements = new ArrayList<>();
    
    public void attach(Element element) {
        elements.add(element);
    }
    
    public void detach(Element element) {
        elements.remove(element);
    }
    
    public void accept(Visitor visitor) {
        for (Element element : elements) {
            element.accept(visitor);
        }
    }
}
```

### Why It's Important
1. **Open/Closed Principle**: You can add new operations without modifying existing classes
2. **Grouping Related Operations**: Visitor groups related operations and separates unrelated ones
3. **Accumulating State**: Visitors can accumulate state as they visit elements
4. **Double Dispatch**: Implements double dispatch in languages like Java that don't natively support it

### Connection to Other Patterns
- **Visitor vs. Command**: Command pattern encapsulates a request as an object, while Visitor represents an operation to be performed on the elements of an object structure
- **Visitor vs. Iterator**: Iterator accesses elements of an aggregate object sequentially, while Visitor performs operations on elements of an object structure





## Class Diagrams: 
Class diagrams represent the structure of a system by showing:
- Classes and their attributes and operations
- Relationships between classes
- Interfaces, packages, and other structural elements



### 1. Classes
A class is represented as a rectangle with three compartments:
- Top: Class name
- Middle: Attributes (properties/fields)
- Bottom: Operations (methods/functions)

```
┌─────────────────┐
│    ClassName    │
├─────────────────┤
│ - attribute1    │
│ # attribute2    │
│ + attribute3    │
├─────────────────┤
│ + operation1()  │
│ # operation2()  │
│ - operation3()  │
└─────────────────┘
```

#### Visibility Modifiers
- `+`: Public
- `-`: Private
- `#`: Protected
- `~`: Package/Default

### 2. Relationships Between Classes

#### Association
Represents a relationship between two classes where one class uses or interacts with another.

```
   Class A ───────────── Class B
```

#### Directed Association
Indicates that one class knows about and uses another class in a specific direction.

```
   Class A ────────────> Class B
```

#### Aggregation
Represents a "whole-part" relationship where one class (the whole) contains references to other classes (the parts), but the parts can exist independently.

```
   Class A ◇─────────── Class B
   (whole)              (part)
```

#### Composition
A stronger form of aggregation where the parts cannot exist without the whole. If the whole is destroyed, the parts are also destroyed.

```
   Class A ◆─────────── Class B
   (whole)              (part)
```

#### Inheritance/Generalization
Represents an "is-a" relationship where one class (the child) inherits from another class (the parent).

```
     ┌────────┐
     │ Parent │
     └────────┘
         ▲
         │
    ┌────────┐
    │ Child  │
    └────────┘
```

#### Realization/Implementation
Shows that a class implements an interface.

```
   ┌────────────┐
   │ «interface»│
   │ Interface  │
   └────────────┘
         ▲
         |
         |
    ┌────────┐
    │  Class │
    └────────┘
```

#### Dependency
Indicates that one class depends on another, but doesn't store a reference to it.

```
   Class A - - - - - -> Class B
```

### 3. Multiplicity/Cardinality
Indicates how many instances of one class relate to an instance of another class.

```
   Class A 1───────0..* Class B
```

Common multiplicity notations:
- `1`: Exactly one
- `0..1`: Zero or one
- `*`: Zero or more (0..*)
- `1..*`: One or more
- `m..n`: From m to n instances

## UML Class Diagram Example 1: Puzzle Game

Based on the 2024 exam question 4, here's a UML class diagram for the puzzle game:

```
┌────────────────┐       ┌───────────────┐
│      Game      │       │    Position   │
├────────────────┤       ├───────────────┤
├────────────────┤       │ - filledCount │
│ + displayRules()│1     │ - gridCells   │
│ + updatePosition()─────┼───────────────┤
└────────────────┘       │ + fillCell()  │
        │                │ + isSolved()  │
        │                └───────────────┘
        │                        │
        │                        │ 1..*
        │                ┌───────────────┐
        │                │    GridCell   │
        │                ├───────────────┤
        │                │ - value       │
        │1..*            │ - position    │
┌───────────────┐        ├───────────────┤
│      Rule     │        │ + getValue()  │
├───────────────┤        │ + setValue()  │
│ # locations   │◆───────│ + isValid()   │
├───────────────┤  1..*  └───────────────┘
│ + isValid()   │                ▲
└───────────────┘                │
        ▲                        │
        │                        │
 ┌──────┴──────┬────────────────┐│
 │             │                │|
┌──────────┐ ┌──────────┐ ┌───────────┐
│RegionRule│ │KillerRule│ │ GivenRule │
├──────────┤ ├──────────┤ ├───────────┤
│          │ │ - total  │ │ - digit   │
├──────────┤ ├──────────┤ ├───────────┤
│+validate()│ │+validate()│ │+validate()│
└──────────┘ └──────────┘ └───────────┘
```
### Puzzle Game UML Analysis (2024 Exam)
This UML represents a classic game structure with separation of game logic (Rules) from game state (Position) and UI representation. The design uses:

- **Inheritance**: Different rule types inherit from a base Rule class
- **Composition**: A Game consists of Rules and a Position
- **Aggregation**: A Position contains GridCells

The design can be improved by:
- Adding a Rule Factory to create different types of rules
- Using a Digits class to encapsulate number validation
- Implementing the State pattern for GridCells
## UML Class Diagram Example 2: Singleton & Factory Patterns

Based on the 2023 exam question 4, here's a UML class diagram representing the Singleton pattern:

```
┌───────────────────────────┐
│        Singleton         │
├───────────────────────────┤
│ - static instance        │
├───────────────────────────┤
│ - Singleton()            │
│ + static getInstance()   │
│ + doSomething()          │
└───────────────────────────┘
```

And here's a Factory pattern:

```
┌─────────────────┐       ┌──────────────────┐
│    Factory      │       │  «interface»     │
├─────────────────┤       │     Product      │
│                 │       ├──────────────────┤
├─────────────────┤       │                  │
│ + createProduct()│─────▶│ + doSomething()  │
└─────────────────┘       └──────────────────┘
                                   ▲
                                   │
                      ┌────────────┴────────────┐
                      │                         │
              ┌───────────────┐         ┌───────────────┐
              │  ConcreteA    │         │  ConcreteB    │
              ├───────────────┤         ├───────────────┤
              │               │         │               │
              ├───────────────┤         ├───────────────┤
              │+doSomething() │         │+doSomething() │
              └───────────────┘         └───────────────┘
```










