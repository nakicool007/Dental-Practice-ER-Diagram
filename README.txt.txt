README.txt
Design Rationale for Dental Practice ER Diagram
-----------------------------------------------

This document explains the reasoning behind the structure of the ER diagram
submitted for the dental practice database design. The focus of this design
was to capture the essential business operations at a conceptual level, as
requested, while leaving room for future refinement and expansion.


1. Overall Design Philosophy
----------------------------
The owners requested that only the “big pieces” of the business be modeled at
this stage. Therefore, the ER diagram prioritizes:

- Conceptual clarity over full normalization
- Major operational workflows over edge cases
- Entities that support reporting and analytics

Details such as exact attributes, timestamps, and transaction-level behavior
were intentionally deferred to a later design phase.


2. Combining Related Concepts Instead of Over-Modeling
-------------------------------------------------------
Several aspects of the business could have been modeled with more granularity,
but were intentionally combined to avoid unnecessary complexity.

- Staff and Salary:
  Salary is modeled as a separate entity but directly tied to Staff rather than
  creating different payroll structures per role. This reflects the business
  rule that all staff are paid monthly with no hourly wages or overtime, making
  additional payroll entities unnecessary at this stage.

- Doctors and Hygienists:
  While these roles share similarities, they were modeled separately rather
  than collapsed into a single “MedicalStaff” entity. This was done to clearly
  represent differences in responsibilities, licensing requirements, and
  participation in procedures and surgeries.


3. Omission of Detailed Loan Modeling
-------------------------------------
The business takes a $300,000 loan to be paid over 10 years. However, the loan
itself is not explicitly modeled as an entity.

This was a deliberate choice because:
- The loan does not affect daily operations
- Its financial impact can be captured through monthly expense reporting
- Detailed amortization schedules would be implementation-level detail

If required later, a Loan entity could be added without altering the rest of
the schema.


4. Medical Records Decomposition
--------------------------------
Instead of modeling a single “MedicalRecord” table, the design separates
clinical activity into:

- Procedures
- Treatments
- Surgeries

This decision reflects real-world differences in:
- Medical complexity
- Billing behavior
- Insurance codes
- Analytics and reporting needs

Keeping these entities separate avoids overloading one entity with unrelated
responsibilities.


5. Scheduling as a Central Operational Entity
---------------------------------------------
Scheduling is modeled as its own entity rather than being embedded within
Patient or Staff.

This design choice allows scheduling to act as a junction between:
- Patients
- Doctors or Hygienists
- Rooms

This accurately reflects real-world constraints and supports daily schedule
views, room utilization tracking, and front-office workflows.


6. Insurance vs Insurance Provider Separation
---------------------------------------------
Insurance information is split into two entities:

- Insurance (patient-specific coverage and subscriber data)
- InsuranceProvider (external companies)

This separation avoids duplication, supports multiple patients per provider,
and enables accurate billing and reporting without violating normalization
principles.


7. Modeling Patient State Explicitly
------------------------------------
Patient State (contacted, scheduled, dormant, etc.) is modeled to support
front-office operations and patient lifecycle tracking.

While state could have been inferred indirectly, modeling it explicitly:
- Improves clarity
- Supports operational reporting
- Enables future analytics on patient engagement


8. Fixed Costs and Monthly Reporting
------------------------------------
Lease, Month, and Building are modeled to support recurring operational costs
and monthly profit/loss reporting.

Supplies and other expenses are not deeply decomposed, as the owners requested
high-level visibility rather than inventory-level tracking at this stage.


9. Intentional Exclusions
-------------------------
The following were intentionally omitted:
- Hourly pay, overtime, and time tracking
- Detailed supply inventory counts
- Fine-grained appointment timestamps
- Regulatory audit history beyond license tracking

These exclusions keep the model aligned with the current business scope and
avoid premature optimization.


10. Extensibility
-----------------
The design supports future expansion, including:
- Advanced analytics and dashboards
- Detailed billing and insurance workflows
- Inventory and loan tracking
- Compliance and audit reporting

No major restructuring would be required to support these additions.


11. Summary
-----------
This ER diagram was designed to balance realism, clarity, and flexibility. Each
modeling decision reflects either an explicit business rule or an intentional
choice to defer complexity until later stages of system design.

The result is a clear, extensible conceptual model that accurately represents
the core operations of a dental practice.
