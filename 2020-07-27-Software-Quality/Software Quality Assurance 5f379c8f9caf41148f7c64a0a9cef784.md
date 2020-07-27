# Software Quality Assurance

- Unit 1
    - IEEE definition
        - A planned and systematic pattern of all actions necessary to provide adequate confidence that an item or product conforms to established technical requirements.
    - Major SQA Activities
        1. Creating an SQA Mgmt Plan
        2. Setting the checkpoints
        3. Applying Software Engineering Techniques
        4. Executing Formal Technical Reviews
        5. Having a multi testing strategy
        6. Enforcing process adherence
        7. Controlling change
        8. Measure Change Impact
        9. Performing SQA Audits
        10. Maintaining Records and Reports
        11. Manage Good Relations
    - SQA Techniques
        1. Auditing
        2. Reviewing
        3. Code Inspection
        4. Design Inspection
        5. Simulation
        6. Functional Testing
        7. Standardization
        8. Static Analysis
        9. Walkthroughs
        10. Path testing
        11. Stress testing
        12. Six sigma
    - Quality Attributes
        - Reliability
        - Maintainability
        - Usability
        - Portability
        - Correctness
        - Efficiency
        - Integrity
        - Testability
        - Flexibility
        - Reusability
        - Interoperability
    - ISO 9126 : Quality external characterisitics
        - Functioning
        - Reliability
        - Usability
        - Efficiency
        - Maintainability
        - Portability
    - SQA Issues
        - Cost
        - Complexity
        - Integration
        - Demand for faster development
        - Defective Software
    - ISO 9001 : Contract b/w two parties → External Standards
    - CMMI Models : Integration Levels

        ![Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/Screenshot_2020-07-27_at_10.57.44_AM.png](Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/Screenshot_2020-07-27_at_10.57.44_AM.png)

    - ISO 15504: Process Assessment

        ![Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/Screenshot_2020-07-27_at_10.39.49_AM.png](Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/Screenshot_2020-07-27_at_10.39.49_AM.png)

        - Not achieved (0–15%)
        - Partially achieved (>15–50%)
        - Largely achieved (>50–85%)
        - Fully achieved (>85–100%).
    - Waterfall model
        1. Reg defn.
        2. Analysis
        3. Design
        4. Coding
        5. System Test
        6. Installation
        7. Operation
    - Prototype model
        - Reqn defn.
        - Prototype design
        - Prototype implementation
        - Prototype evaluation by customer
        - Demands for correction
        - System Test
        - System Conversion
    - OOP model
        - Req Defn.
        - OO Analysis
        - OO Design
        - Reusability survey of lib
        - System Construct
        - Test
    - McCall's Factor Model Tree
        - Product Transition
            - Portability
            - Reusability
            - Interoperability
        - Product Operation
            - Correctness
            - Efficiency
            - Reliability
            - Integrity
        - Product Revision
            - Flexibility
            - Festability
            - Maintainability
    - Advanced Spiral Model

        ![Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/1200px-Spiral_model_(Boehm_1988).svg.png](Software%20Quality%20Assurance%205f379c8f9caf41148f7c64a0a9cef784/1200px-Spiral_model_(Boehm_1988).svg.png)

- Unit 2
    - Configuration Auditing : The configuration audit is an activity that is conducted to determine that a system or item meets it functional requirements and has been built in accordance with its blueprints, source code, or other technical documents. Conducted at the end of each life cycle phase. Two types :
        - Functional Audit
        - Physical Audit
    - Configuration Mgmt Metrics:
        - Frequency of updates
        - Release downtime metrics
        - Average number of errors
        - Code lines per update
        - Rework metrics
        - Frequently Changing Files
        - Root Causes for late delivery
- Unit 3
    - Risk Management
        - ***Identify*** risks and their triggers
        - ***Classify*** and prioritize all risks
        - Craft a ***plan*** that links each risk to a mitigation
        - ***Monitor*** for risk triggers during the project
        - Implement the ***mitigating action*** if any risk materializes
        - ***Communicate*** risk status throughout project
    - Identification of Defect
    - Analysis of Defect
    - Correction of Defect
    - Implementation of Correction
    - Regression Testing
        - Types
            - Unit Regression
            - Partial Regression
            - Complete Regression
    - Categorization of Defect

        Severity / Impact

        Probability / Visibility

        Priority / Urgency  

    - Relationship of Development Phases
- Unit 4
    - Traceability
        - Traceability in software engineering describes the extent to which documentation or code can be traced back to its point of origin. The goal of traceability is to provide better quality and consistency of product development. It brings the ability to verify the history, location, and application of an item by means of documented identification. Two types : Chain Traceability and Internal Traceability
        - Characterisitics
            - Origin Points
            - Key Associations
            - Forward and Back
            - Technical Specificity
            - Auditability
    - Records
    - Software Quality Program Planning
        - Two levels → Organisational and Project
        - Covers the following issues :

            Quality objectives and goals
            The overall objectives of the quality management programme together with measurable goals
            to be achieved
            • Quality management system scope
            Who and what will be impacted by the quality management system. For example: process
            scope, product scope, organisational scope.
            • Organisation & responsibilities
            Organisational structure, reporting relationships and roles and responsibilities for quality
            • Resource requirements
            Identification of the people and resources required to develop, use, maintain and improve the
            quality management system
            • Cost benefit analysis
            A quality program cost benefit analysis addressing issues such as: the cost of poor quality, the
            cost to improve quality and the cost benefits to be achieved
            • Activities and deliverables
            The quality management system elements will be produced/improved The quality management
            system development activities required
            • Schedule
            The timeframes in which the work will be achieved together with major milestones for quality
            management system element delivery, review and deployment.
            • Risk analysis
            An analysis of what could go wrong together with strategies for risk reduction.

    - Accuracy

        The ability of the system to produce accurate results (and to what level of accuracy this is required).

    - Authority
        - To determine if the source author, creator, or publisher of the information is the most knowledgeable.
    - Benefit
        1. Saves you money
        2. Maintains great user experience
        3. Boosts customer satisfaction
        4. Organizational productivity and efficiency
    - Communication
        - Improving interpersonnel communication
        - Interference
            1. Preconceptions and Opinions
            2. Personality Conflicts
            3. Jargon
            4. Mixed Meanings
        - Feedback
    - Consistency
    - Retaliation
- Practical end
    - Cohesion vs Coupling
        - Cohesion is the indication of the relationship within the module. Coupling is the indication of the relationships between modules
    - CK Metric Suite
        - WMC → Weighted Methods Per Class → Keep down → High means, more application specific
        - DIT → Depth of Inheritance Tree → Design Complexity → High DIT, more faults → Middle layer classes, higher number of faults → ≤ 5
        - NOC → Number of Children → High reuse of base class. Inheritance is a form of reuse → Base class may require more testing → Improper abstraction of the parent class → Misuse of sub-classing. In such a case, it may be necessary to group related classes and introduce another level of inheritance
            - A class with a high NOC and a high WMC indicates complexity at the top of the class hierarchy. The class is potentially influencing a large number of descendant classes. This can be a sign of poor design. A redesign may be required.
        - CBO → Coupling between Objects
            - Two classes are coupled when methods declared in one class use methods or instance variables defined by the other class.
            - High CBO is undesirable. Excessive coupling between object classes is detrimental to modular design and prevents reuse. The more independent a class is, the easier it is to reuse it in another application. In order to improve modularity and promote encapsulation, inter-object class couples should be kept to a minimum.
        - RFC → The response set of a class is a set of methods that can potentially be executed in response to a message received by an object of that class. RFC is simply the number of methods in the set.
        - LCOM → Lack of cohestion of methods
            - It is an important measure because it indicates whether the present set of methods should be together in a class or could be split to form two or more cohesive classes.