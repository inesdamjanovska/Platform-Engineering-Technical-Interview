# Platform-Engineering-Technical-Interview

## Level: JL4 – Engineer
Sheet: JL4-2026-06-30-134822

Candidate name: Ines Damjanovska 

Instructions:

	• Section A (10 questions, 1 mark each): circle the letter of the correct answer.
	• Section B Part 1: answer both questions in the space provided.

### Questions - Section A:

1. A function stamps every fabrication log entry with the current time, and an engineer’s
test for it passes in the morning but fails near midnight as the date rolls over. The team
wants the test to behave the same regardless of when it runs. To test a function that
reads the system clock, you...

		B. Inject or mock the time source

Code snippet - Testing code that reads system clock
```
from datetime import datetime

def stamp_log_entry(message, current_time):
    return f"{current_time.isoformat()} {message}"

def test_stamp_log_entry():
    fake_time = datetime(2026, 7, 7, 23, 59, 59)

    result = stamp_log_entry(
        "System started",
        fake_time
    )

    assert result.startswith("2026-07-07T23:59:59")
```
2. While reading the team’s pytest suite, a new hire notices many tests request the same
named helpers that the framework calls fixtures, and asks what a fixture actually does
for a test. In pytest, a fixture provides...

		C. Reusable setup/teardown for tests

Code snippet - pytest fixture

```
import pytest

@pytest.fixture
def sample_user():
    return {"name": "Ines", "role": "engineer"}

def test_user_role(sample_user):
    assert sample_user["role"] == "engineer"
```

3. After finishing a cell layout, an engineer needs to prove that what she drew actually
implements the transistors and connections in the schematic, not merely that the shapes
are legal. She works through the verification flow to pick the right check for that job.
Which check confirms the layout matches the schematic netlist?

		A. LVS

4. Tuning an analog block, an engineer adjusts the W and L values on a Metal-Oxide-
Semiconductor Field-Effect Transistor (MOSFET) instance and watches the drive current change.
A colleague new to device design asks what those two parameters actually
correspond to. For a MOSFET, the parameters W and L refer to...

		C. Transistor channel width and length

5. During a code review on the deck-automation tool, a senior engineer flags a sprawling
helper and cites the Single Responsibility Principle (SRP). To confirm the new hire
grasped the feedback, she poses a quick definition check. The SRP says a unit should...

		A. Have one reason to change

6. Debugging a flaky unit test on the metrics tool, an engineer suspects one function is not
behaving consistently between runs. A colleague suggests rewriting it as a ’pure function’
and first checks that the team agrees on what that term means. A ’pure function’...

		D. Returns the same output for the same input with no side effects

7. Your team has just enabled GitHub Copilot, and you watch it autocomplete an entire
function in seconds. It is tempting to accept everything, but these Artificial Intelligence
(AI) assistants sometimes produce plausible-looking yet wrong code. Thinking about
good practice, using GitHub Copilot or other AI assistants, you should...

		D. Use it to help, but review, test and verify the output

8. A colleague promised to review your migration script, but two days have passed with
no response and your Task is frozen. The sprint is ticking by, your stand-up update
keeps reading ’still blocked,’ and you sense you cannot simply keep waiting. You’ve
been blocked waiting on someone for two days. Best action?

		A. Raise it as an Issue and seek the right person

9. A new engineer is about to complete their first Pull Request (PR) at GlobalFoundries
(GF) and wants to get it right the first time, because the branch policy will block the
merge button until every required condition is met. They have heard there are several
gates - approvals, linkage, build status, merge style - and are trying to recall the exact
set the team enforces. Which combination satisfies the team’s PR review policy?

		B. 2 approvals, linked item, resolved comments, rebase & fast-forward, successful build

10. At GlobalFoundries (GF), a new platform team is told their next deliverable will be a
Domain-Specific Language (DSL) for capturing design rules, rather than another pile
of Python scripts. A junior engineer, hearing the term for the first time in a kickoff
meeting, wants to nail down the basic concept before diving in. A DSL is...

		D. A language tailored to a specific problem domain

### Section B:

1. A new engineer at the foundry watches cards glide across the Azure DevOps (ADO)
board during a sprint and can see the column names but not yet grasp what each
transition signifies about the underlying work. In an onboarding session, their mentor
asks them to narrate the journey of a typical work item in their own words. Explain the
New -¿ Active -¿ Review -¿ Closed work-item flow.

A work item represents a task, feature, or bug that needs to be completed. The different statuses show the progress of the task during development.

**New**

The task has been created, but nobody has started working on it yet.

Example: A team creates a task called "Add user login functionality." The task is waiting to be assigned and started.

**Active**

The task is currently being worked on by a developer. The developer writes code, makes changes, and tests the solution.

Example: A developer starts implementing the login functionality and creates the required code.

**Review**

The development work is finished, but the changes need to be checked before they are added to the main project. Other team members review the code and make sure everything works correctly.

Example: A developer creates a Pull Request and waits for approval from the team.

**Closed**

The task is completed. The code has been approved, tests have passed, and the changes have been merged into the main branch.

Example: The login feature is finished and ready to be used.

2. A project lead maps out the remaining schedule and points to the wall of verification a
block must clear before it can be released to the fab. A newer engineer, who has only
ever run a single check on her own cell, asks for the big-picture sequence of sign-off steps
that stand between a finished layout and the handoff. At a high level, what verification
does a layout go through before tape-out?


Before a chip can be sent to the factory for production, the completed design needs to go through several verification steps. These checks make sure that the chip is designed correctly, follows manufacturing rules, and works as expected.

The process starts with the layout.

		Layout

The layout is the physical design of the chip. It shows where the different components, such as transistors and wires, are placed on the chip.

It represents how the circuit will be physically built. Before manufacturing, the layout needs to be checked to make sure there are no problems.

---

		DRC (Design Rule Check)

DRC verifies that the layout follows the rules required by the semiconductor factory.

It checks things like the distance between wires, the size of different layers, and whether components are placed correctly.

For example, if two wires are too close together, it can create problems during manufacturing. DRC detects these problems before the chip is produced.

---

		LVS (Layout Versus Schematic)

LVS compares the final layout with the original schematic, which represents the intended circuit design.

The purpose of LVS is to make sure that the physical layout contains the same components and connections as the original design.

For example, if the schematic contains 10 transistors but the layout contains only 9, LVS will detect the mismatch.

---

		PEX (Parasitic Extraction)

PEX extracts the additional electrical effects that appear because of the physical layout.

In a real chip, wires are not perfect and can introduce small effects such as resistance and capacitance.

PEX calculates these values so they can be included in simulations and provide a more realistic view of how the chip will behave.

---

		Post-layout Simulation

After PEX, the extracted information is added to the simulation process.

This allows engineers to test the chip under more realistic conditions and verify that it still works correctly.

The simulation checks important factors such as timing, performance, and power consumption.

---

		Sign-off Verification

Before manufacturing, the design goes through final verification checks.

These checks confirm that the design is ready for production and that no major issues remain.

---

		Tape-out

Tape-out is the final step before manufacturing.

After all verification steps are completed successfully, the final design files are sent to the factory for chip production.


