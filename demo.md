# The Anatomy of an AI Agent — Hands-on Demo

**Updated:** November 2, 2026  
**Platform:** Microsoft 365 Copilot Agent Builder + SharePoint  
**Agent:** `Conference Prep Guide`  
**Sample skill:** `Conference-Travel-Worksheet`

This walkthrough builds **one agent in stages**. You'll see what instructions can do on their own, what changes when you connect company documents, and how an agent can invoke a task-specific skill without using it for every question.

Everything about **Contoso Dev Conference**, its hotels, and Contoso's travel policy is **fictional sample data**. You do not need access to the presenter's SharePoint tenant. Use a SharePoint site you control and create the three small sample Word documents using the content in this README. No real travel request, approval, reservation, or payment is made.

> **Reproduction note:** The prompts, scenario, and expected results match the current conference demonstrations. UI labels and skill availability may vary by tenant and rollout.

## What you will build

| Demo | Add to the same agent | What you'll test |
| --- | --- | --- |
| **1. Instructions** | Basic instructions, then improved instructions | How instructions affect behavior but cannot establish an unknown corporate policy |
| **2. Knowledge** | Three SharePoint Word documents | Retrieval, evidence and citations, hotel comparisons, and conversation context |
| **3. Skill** | `Conference-Travel-Worksheet` | Normal questions without a worksheet; then an explicit request that creates an advisory worksheet |

---

## 1. Prerequisites, licensing and possible costs — read before starting

### Required access and permissions

- **Microsoft 365 work or school account** in an organization where **Agent Builder** is enabled for you. Use the web or desktop experience, not the mobile app. Start at [Microsoft 365 Copilot Chat](https://m365.cloud.microsoft/chat) and look for **Agents & Skills** / **New agent** (the navigation may differ).
- **Eligible license or enabled usage-based access.** Your tenant admin must confirm that your license and billing configuration support Agent Builder **and SharePoint knowledge grounding**. Access to basic Copilot Chat does *not* automatically guarantee that all three demos will work.
- **SharePoint Online site/document library** where you can create or upload three `.docx` files and read them with your signed-in account. You must be able to select those files as knowledge sources. Ask a site owner for access rather than using someone else's documents.
- **Agent skills capability enabled** for Demo 3. Skill authoring/availability is controlled by licensing, tenant policies, and product rollout. Microsoft's preview guidance has also required **Microsoft Frontier program** participation. If you do not see the Skills section, consult your administrator and current Microsoft documentation; don't assume the feature is enabled for your tenant.

### Cost and licensing checkpoints

| Item | Possible cost / what to check |
| --- | --- |
| Microsoft 365 / SharePoint | An eligible paid organizational subscription may be needed. If you already have one, making three small sample Word files normally doesn't require buying a separate SharePoint service. Storage is subject to tenant limits. |
| Microsoft 365 Copilot license | A paid **Microsoft 365 Copilot add-on** is one qualifying path. Confirm whether your assigned license includes the necessary agent and SharePoint-grounded functionality. The subscription itself is a cost. |
| Pay-as-you-go alternative | **Potential metered Copilot Credits charges.** Some eligible organizations enable usage-based billing for agents that access SharePoint or other shared tenant data. This requires administrator configuration and an associated billing arrangement; do **not** activate pay-as-you-go without approval. |
| Demo 1 (instructions only) | Instruction-grounded agents can be available at no additional *agent consumption* charge under eligible Copilot Chat access. You still need a qualifying Microsoft 365 environment. |
| Demos 2 and 3 (SharePoint grounding) | **Potential charges** without the full Copilot add-on, where PAYG is available; each interaction may use metered capabilities. Licensed use may be included for eligible employee-facing scenarios. Verify your specific tenant's entitlement and billing policy. |
| Demo 3 (skills) | Skill access may be unavailable even when Demos 1 and 2 work. Usage may be subject to your licensing / PAYG arrangement and to the capabilities the skill invokes. This README's example does not use any paid third-party API or external booking service. |
| Hotel amounts mentioned below | **$225 per night and $900 for the stay are fictional travel expense examples, not fees charged for these demos.** |

**There is no reliable universal “cost per run” for this walkthrough.** Any metered amount depends on your tenant's licensing, agent design and consumption. Before trying the SharePoint steps, ask your administrator whether a **Microsoft 365 Copilot license or approved PAYG billing policy** covers your account, and whether spending limits or monitoring are configured. The safest approach is to use an existing licensed sandbox with administrator approval.

Current Microsoft reference pages (review them for changes):

- [Agent Builder overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder)
- [Build agents in Agent Builder](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-build-agents)
- [Knowledge sources in Agent Builder](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-add-knowledge)
- [Add skills in Agent Builder](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-add-skills)
- [Plan licensing and cost](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/cost-considerations)
- [Copilot Credits / billing rates](https://learn.microsoft.com/en-us/microsoft-copilot-studio/requirements-messages-management)

### Before you proceed

- [ ] I can open Agent Builder and create or edit an agent.
- [ ] I can create and view `.docx` files in a SharePoint site I control.
- [ ] I've confirmed my account can use SharePoint sources in agents, and any usage-based billing is authorized.
- [ ] For Demo 3, I've confirmed that **Skills** are actually available in my environment.
- [ ] I'm using only fictional demo information, not confidential company policies.

If you lack the skill feature, **complete Demos 1 and 2** and read the Demo 3 skill specification as a conceptual exercise. Adding the skill text to ordinary agent instructions is *not* an equivalent test of skill invocation.

---

## 2. Create the sample SharePoint documents

Create a folder (for example, `ConferencePrepDemo`) in a SharePoint document library to which you have access. Create **three Word documents** with these exact filenames and the following sample contents. You can copy the text into Word and save each document as `.docx`.

### File A: `Conference-Details-2027.docx`

**Paste this formatted content into the Word document:**

#### Contoso Dev Conference 2027

##### Conference Information

Conference: Contoso Dev Conference 2027

Location: Chicago, Illinois, USA

Conference dates: October 12–15, 2027

Venue: Lakeshore Convention Center, Chicago

##### Conference Hotels

The following hotels are recommended accommodations for attendees of Contoso Dev Conference 2027 in Chicago. Conference room rates are available to registered attendees, subject to room availability.

| Hotel | Location | Conference room rate |
| --- | --- | --- |
| West Loop Hotel | Chicago, Illinois | $225 USD per night |
| Lakeshore Hotel | Near the conference venue, Chicago, Illinois | $250 USD per night |
| Magnificent Mile Suites | Chicago, Illinois | $310 USD per night |

Hotel information:

- Rate type: Standard room, single or double occupancy
- Taxes and fees: Not included in the nightly room rates
- Availability: Subject to availability at the time of booking
- Booking: Hotel reservations must follow the company's corporate travel policy and approval requirements

These are recommended accommodation options, not confirmation that each hotel complies with the company's lodging policy. Employees should compare their selected hotel's nightly rate with the applicable corporate lodging limit before requesting approval or making reservations.

##### Booking Considerations

Attendees should review the hotel's cancellation terms and confirm the total cost before making a reservation.

The conference hotel rate does not automatically mean the accommodation complies with an attendee's employer's travel policy.

Employees should consult their organization's travel policy and complete any required approvals before booking.

##### Additional Information

Conference registration and hotel reservations are separate processes.

This document provides conference information for planning purposes only and does not confirm hotel availability or authorize travel.

### File B: `Corporate-Travel-Policy-2027.docx`

**Paste this formatted content into the Word document:**

#### Contoso Corporate Travel Policy 2027

##### 1. Purpose

This policy establishes the requirements for employee business travel, including conference attendance, accommodation expenses, approvals, and reservations.

The policy applies to all Contoso employees traveling on company business.

##### 2. Hotel Accommodation Limits

Employees must select accommodation that complies with the company's approved nightly lodging limits.

For business travel to Chicago, Illinois, the maximum permitted hotel room rate is $275 USD per night, excluding applicable taxes and mandatory hotel fees.

The nightly lodging limit applies to the base room rate, not the total cost of the stay.

A hotel rate below the nightly limit does not automatically authorize a reservation.

##### 3. Travel Approval Requirements

Employees must obtain manager approval before making any travel reservations, including hotel bookings.

The required process is:

1. Prepare a business travel request that identifies the purpose, destination, dates, and estimated costs.
2. Submit the travel request through the company's approved travel-request process.
3. Obtain approval from the employee's manager.
4. Make reservations only after approval has been granted.

Employees must not interpret an AI-generated response as an official travel approval.

##### 4. Booking Requirements

After receiving manager approval, employees must book accommodation through the company's approved corporate booking channel.

Employees should confirm room availability, cancellation conditions, taxes, mandatory fees, and the estimated total cost before completing a reservation.

##### 5. Exceptions

If the proposed hotel's base nightly rate exceeds the applicable lodging limit, employees must request and receive an approved exception before booking.

An exception request must explain the business reason for exceeding the limit.

##### 6. Policy Verification

Employees are responsible for confirming that their proposed travel arrangements comply with the current corporate travel policy.

An informational response from an AI assistant does not constitute approval, submission of a travel request, or confirmation of a reservation.

### File C: `Conference-Travel-Checklist-2027.docx`

**Paste this formatted content into the Word document:**

#### Contoso Conference Travel Checklist 2027

##### Purpose

This checklist helps Contoso employees prepare for business conference travel and complete the required approval and booking steps.

Employees should use this checklist alongside the current Corporate Travel Policy and the information provided by the conference organizer.

##### 1. Confirm Conference Details

- Confirm the conference name, location, and dates.
- Identify the conference venue and recommended accommodation.
- Determine the required arrival and departure dates.
- Confirm the conference registration requirements.

##### 2. Review Accommodation Options

- Check the recommended conference hotel's nightly room rate.
- Compare the base nightly rate against the applicable corporate lodging limit.
- Estimate the total accommodation cost based on the number of nights.
- Identify applicable taxes and mandatory hotel fees.
- Review room availability and cancellation conditions.

Important: A hotel rate that meets the company's spending limit does not automatically authorize a reservation.

##### 3. Prepare the Travel Request

Before making reservations:

- Document the business purpose of the trip.
- Record the destination and planned travel dates.
- Identify the proposed hotel and estimated accommodation cost.
- Include other anticipated travel expenses, where applicable.
- Submit the travel request through Contoso's approved travel-request process.

##### 4. Obtain Manager Approval

- Wait for the manager to review the submitted travel request.
- Confirm that manager approval has been granted.
- If the hotel exceeds the lodging limit, obtain an approved exception before booking.

Do not book travel before receiving the required approval.

##### 5. Complete Reservations

After approval:

- Use Contoso's approved corporate booking channel.
- Confirm the hotel rate, dates, and cancellation terms.
- Complete the reservation.
- Retain the booking confirmation and relevant receipts.

##### 6. Verify Completion

Before considering the arrangements complete:

- Confirm that the travel request was submitted successfully.
- Confirm that manager approval was recorded.
- Confirm that a hotel reservation exists in the approved booking system.
- Verify the reservation dates and accommodation details.

An AI assistant explaining these steps does not mean that the travel request was submitted, approval was granted, or a reservation was completed.

##### Additional Guidance

If any required information is missing, employees should consult the appropriate conference documents, corporate travel policy, or travel administrator before proceeding.

**Verify the files:** Open all three from SharePoint after saving. Confirm that the three hotel rates are **$225, $250 and $310** and the Chicago base-rate limit is **$275**. Do not add these files as agent knowledge until Demo 2.

---

## 3. Demo 1 — See what instructions do (and do not do)

### Step 1: Create one agent

1. Open [Microsoft 365 Copilot Chat](https://m365.cloud.microsoft/chat) on the web with your work or school account.
2. Select **Agents** in the left-hand navigation, then select **New agent** from its submenu.
3. In the initial agent-builder chat view, select **Skip** on the right-hand side, above the chat input area, to open the configuration interface. **Skip is a separate button above the input, not a control inside the chat input.**
4. Set the **name** to `Conference Prep Guide`.
5. Set the description to: `Helps employees prepare for conferences and business travel, identify information they need, and check what can be verified.`
6. For the first test, use these intentionally minimal instructions:

   ```text
   You help employees prepare for conferences and business travel.
   Provide useful travel-planning advice.
   ```

7. Under **Work content**, turn off **Cloud files**, **Outlook**, and **Teams**. Do not add SharePoint documents, a skill, or other organizational knowledge yet. The first demo should test instructions without access to company content.
8. Click **Create** near the **top-right corner** of Agent Builder to create the agent.
9. Open the agent in chat (or its **Try it** experience).

### Step 2: Ask the initial questions

**Prompt 1:**

```text
I'm attending a conference in Chicago. What should I check before booking a hotel?
```

**Expected:** Broadly useful travel-planning advice about what to check before booking a hotel.

**Prompt 2:**

```text
What is our company's exact Chicago nightly hotel limit?
```

**Expected:** The agent cannot verify Contoso's exact Chicago hotel limit at this stage, because organizational knowledge has not been enabled. If it gives a specific number, treat that as an unverified claim, not evidence that it found the policy.

### Step 3: Improve the same agent's instructions

Edit **Conference Prep Guide** and replace its instructions with the following:

```text
You are Conference Prep Guide, an assistant helping employees prepare for business conferences and travel.

Provide practical, concise travel-preparation guidance.

Use available organizational sources when possible, and clearly distinguish verified company information from general advice.

When answering questions using knowledge sources, retrieve the relevant source
content again rather than relying solely on previously retrieved information.
This is especially important when source documents may have changed recently.

Never invent a corporate policy, spending limit, approval requirement, or booking confirmation.

If company-specific information is unavailable, explicitly state that you cannot verify it and explain what the employee should check next.

Do not claim to approve requests, make reservations, or perform other actions unless you have actually completed those actions using an available tool.

For ordinary responses, use these three headings:
- What I can confirm
- What I cannot verify
- What you should do next

When a specialized skill specifies its own output format, follow the skill's
format instead of these three headings.
```

Click **Update** in the **top-right corner** of Agent Builder to save the revised instructions. **Start a new conversation** with the same agent (using **New conversation** or the equivalent control in your environment). Then **repeat the exact same two prompts**. This keeps the first test's conversation context from affecting the second test.

**Check:** The agent should follow the three-heading format and clearly state that the corporate lodging limit is not yet verified. This is an instruction change, **not** a knowledge change.

**Format carries forward:** The ordinary-response format remains in effect throughout Demos 2 and 3. It comes from the agent instructions, not from adding SharePoint knowledge or a skill. When the skill is invoked, its worksheet format takes precedence.

---

## 4. Demo 2 — Add SharePoint knowledge and use conversation context

### Step 1: Add the three documents

1. Edit the **same** `Conference Prep Guide` agent.
2. Under **Configure**, open **Knowledge**, and click **Add knowledge**.
3. **Preferred — SharePoint-connected knowledge:** Choose **Cloud files / Work content** in the file picker. Find the three `.docx` documents in your SharePoint folder and select the exact three files. Avoid selecting a broad unrelated site.
4. If all three files are available, add them, save the agent, and start a **new conversation** for Demo 2. Continue to Step 2.

**SharePoint indexing delay:** After creating or uploading documents to SharePoint, it may take some time before they appear in Agent Builder when you select **Add knowledge → Cloud files / Work content**. This is because newly added files may not yet have been indexed and made available for discovery. If you cannot find the three conference documents, you can use the temporary attachment workaround below to continue the demo. You can return later to replace the attachments with the SharePoint files once they become available. Keep in mind that missing files can also be caused by permissions, licensing, or tenant configuration issues.

**Temporary workaround — files are not listed in Cloud files / Work content:**

1. **Download the three Word documents from SharePoint to your computer.** They were already created and verified in Section 2; don't repeat the document-access verification here.
2. In Agent Builder's **Knowledge** section, scroll toward the **bottom** to find **Attachments** and add the three locally downloaded `.docx` files there, **rather than** selecting them through **Cloud files / Work content**.
3. Wait until the attachments finish **Preparing**, if that status is displayed. Confirm that all three attached files are available, save the agent, and start a **new conversation**.
4. Continue with the Demo 2 prompts. During this temporary stage, describe the responses as grounded in **attached document copies**, not as evidence of successful SharePoint-connected retrieval. The expected hotel facts and policy comparisons remain the same; SharePoint-specific citations and freshness behavior are not validated by this fallback.

**Switch back to SharePoint later:**

1. Later that day or the next day, check **Cloud files / Work content** again. Do not treat this timeframe as guaranteed.
2. Once the three SharePoint files are selectable, edit the agent, **remove the temporary attachments**, and select the three SharePoint files from Cloud files / Work content. Ensure the attachment copies and the SharePoint versions are not both left as active knowledge sources.
3. Save the agent, start a **fresh conversation**, repeat the Demo 2 hotel/policy question, and inspect citations or other available source details to confirm that the agent used the SharePoint documents.

**Note:** If the files remain missing, recheck licensing, SharePoint permissions, sign-in, administrative policies, and the selected tenant. The attachment fallback does not repair those problems. Where supported, SharePoint URLs may offer another configuration route, but document URLs with browser-specific query strings are not always accepted.

### Step 2: Prompt 1 — compare the hotels and the policy

**Paste this prompt:**

```text
I'm attending Contoso Dev Conference in Chicago. What are the recommended conference hotels, which ones meet our corporate nightly lodging-rate limit, and what approval is required before booking?
```

**Expected outcome:**

| Hotel | Rate (USD/night, base) | $275 Chicago limit |
| --- | ---: | --- |
| West Loop Hotel | $225 | Meets limit ($50 below) |
| Lakeshore Hotel | $250 | Meets limit ($25 below) |
| Magnificent Mile Suites | $310 | Exceeds limit ($35 above); approved exception required |

The response should also identify the requirement to **submit a travel request and obtain manager approval before booking any hotel**, then use the approved corporate booking channel. When SharePoint knowledge is configured, the agent should cite the relevant SharePoint documents. It should **not** claim a room is available or that approval has been granted.

**Check the evidence:** After the preferred SharePoint source has been selected or restored, open the citations to `Conference-Details-2027.docx` and `Corporate-Travel-Policy-2027.docx` to demonstrate SharePoint retrieval. During the temporary attachment fallback, verify the uploaded content and label the result as attachment-grounded instead.

**Source freshness:** This instruction is based on a presenter observation: shortly after a SharePoint conference document was edited from one recommended hotel to three, the agent initially returned the old one-hotel answer; explicitly asking it to retrieve the knowledge again corrected the result in that test. Re-retrieval does **not** bypass indexing delays or guarantee access to the newest revision. If an answer appears stale, open the citations, inspect the actual source and any available effective dates, last-modified dates, or version information. Treat the response as what the accessible sources say, not proof that Contoso's policy has not changed.

### Step 3: Prompt 2 — choose a hotel and calculate the stay

**Stay in the same conversation and paste:**

```text
I'd like to stay at the West Loop Hotel. If I check in on October 12 and check out on October 16, what would my room cost before taxes and fees?
```

**Expected:** October 12–16, 2027 is **4 nights**, so **4 × $225 = $900 USD** before taxes and fees. The agent should use your chosen hotel and the context from this chat, distinguish the verified *base rate* from actual availability, and repeat that approval is needed before booking.

**Check:** A hotel selection within a conversation is **conversation context**. It does not establish cross-chat persistent memory.

---

## 5. Demo 3 — Add a skill, then invoke it selectively

**How this demo is structured:** Three prompts in one conversation are designed to show that the skill is selective. Prompts 1 and 2 establish hotel options and a selection — ordinary knowledge questions that the agent should answer without invoking the skill. Prompt 3 is the first explicit request for a worksheet, which should trigger the skill. The teaching point is that the skill activates on request, not automatically for any hotel or travel question.

### Step 1: Prepare the skill

Continue using **the same agent** and the three conference knowledge documents. Prefer the SharePoint files selected through Cloud files / Work content. If you are still using temporary attachments because SharePoint discovery has not completed, you can test skill selection and worksheet generation, but this does **not** verify SharePoint-connected retrieval. Once the SharePoint files become available, replace the attachments and repeat the knowledge and skill tests in fresh conversations. You need **Skills** access in Agent Builder for this step.

**Create the skill through Agent Builder's chat-based skill-creation experience:**

1. In `Conference Prep Guide`, open **Configure → Skills** and choose the option to add or create a skill. In the skill-creation experience, select its chat-based option to describe the skill. UI labels and placement can vary by tenant; follow the current on-screen creation flow. If no chat-based creation option is available, check your tenant's current Skills availability rather than substituting general agent instructions.
2. Paste the prompt below into the skill-creation chat. It is a practical prompt reconstructed from the skill specification for this demo, **not an exact transcript** of the earlier preparation conversation.

```text
Create a skill named Conference-Travel-Worksheet.

Description and activation:
Use this skill only when the user explicitly asks for a conference travel
worksheet, conference travel approval worksheet, travel authorization
worksheet, or approval worksheet for a conference trip. Do not activate it
for ordinary hotel questions, policy questions, cost estimates, or questions
about whether approval is required.

Sources and conversation details:
- Retrieve relevant available knowledge sources for conference details,
  hotel rates, the corporate travel policy, and the conference travel checklist.
- Use relevant trip details already established in the current conversation,
  such as the selected hotel and check-in/check-out dates.
- Cite knowledge sources where available. Distinguish source facts,
  calculations, and unknown information.
- Do not invent missing values, approvals, bookings, or evidence.

Calculations and readiness criteria:
- Calculate nights from check-in and check-out dates. Multiply the number of
  nights by the verified base nightly room rate; exclude taxes and fees unless
  their amounts are known.
- Lodging compliance: PASS when the verified base nightly rate is at or below
  the applicable nightly limit; FAIL when it is above the limit without an
  approved exception; otherwise INCOMPLETE. An above-limit hotel requires an
  approved exception before booking.
- Budget completeness: PASS only when all relevant expected costs are
  reasonably supplied; otherwise INCOMPLETE.
- Approval status: APPROVED only with reliable evidence of manager approval;
  otherwise PENDING. A statement in chat is not itself proof of approval.
- Booking information: COMPLETE only when applicable availability, full
  price, booking details, and cancellation terms are verified; otherwise
  INCOMPLETE.
- Travel preparation: COMPLETE only when the business purpose, required
  request steps, expense details, and other checklist requirements have been
  addressed; otherwise INCOMPLETE.
- Overall readiness is READY only when lodging compliance is PASS, budget
  completeness is PASS, approval is APPROVED, booking information is COMPLETE,
  and travel preparation is COMPLETE. Otherwise it is INCOMPLETE.

Worksheet output:
Produce the worksheet directly in chat with this exact title:
CONTOSO — CONFERENCE TRAVEL APPROVAL WORKSHEET

Put this advisory subtitle directly beneath the title:
Advisory assessment only — not an approved travel request or authorization to book.

Use these sections, in this order:
1. Travel Details: conference, location, dates, venue, hotel, check-in,
   check-out, number of nights, room type, and business purpose.
2. Estimated Travel Expenses: nightly base rate, number of nights, base
   lodging total, known and unknown taxes/fees, registration, transport,
   meals, and other costs.
3. Travel Readiness Assessment: a table with all five criteria, their
   statuses, and short evidence-based explanations.
4. Overall Readiness Classification: READY or INCOMPLETE.
5. Outstanding Requirements / Next Steps.
6. Sources.

Clearly label unknowns and keep the worksheet concise. This is an advisory
readiness assessment, not authorization. Never imply that a reservation or
approval exists without evidence. Do not submit a travel request, approve
travel, book a hotel, or charge a payment.
```

3. Review the generated skill before saving. Confirm its name is `Conference-Travel-Worksheet`; its description activates only on explicit worksheet requests; it retrieves the relevant knowledge and uses trip details from the current conversation; its calculation and status rules match the prompt; it includes all five readiness criteria, the required worksheet sections, and the advisory safety language.
4. Use the skill editor's **Save**, **Add**, or equivalent action to add the reviewed skill to `Conference Prep Guide`. Confirm it appears in the agent's Skills list. Do not replace the agent's general instructions with the skill text; a real skill is distinct from general instructions.
5. If Skills or chat-based creation is unavailable, revisit the prerequisites and current tenant documentation. Do not simulate skill invocation by pasting the worksheet instructions into the agent's general instructions.

The generated skill follows model instructions; it is not mathematically enforced deterministic code. Wording and behavior may vary, so verify the classifications and actual skill invocation during the tests below.

### Step 2: Start a fresh conversation

Start **a new conversation** with the same agent, now containing the three sources **and** the skill. Do **not** assume the West Loop selection from Demo 2 exists in this new chat.

### Step 3: Prompt 1 — an ordinary knowledge question

> **Note:** Prompts 1 and 2 below are intentionally the same as Demo 2. The goal is to watch that the skill does **not** activate for ordinary hotel and policy questions — that selective non-invocation is what this demo is designed to show before Prompt 3 triggers the skill explicitly.

```text
I'm attending Contoso Dev Conference in Chicago. What are the recommended conference hotels, which ones meet our corporate nightly lodging-rate limit, and what approval is required before booking?
```

**Expected:** The same three hotels, nightly-limit comparison, and approval information as Demo 2. **No travel approval worksheet** should be produced.

### Step 4: Prompt 2 — an ordinary hotel selection and estimate

**Stay in the same conversation:**

```text
I'd like to stay at the West Loop Hotel. If I check in on October 12 and check out on October 16, what would my room cost before taxes and fees?

```

**Expected:** **West Loop Hotel, 4 nights, $900 USD before taxes and fees**. **No worksheet** should be produced yet.

### Step 5: Prompt 3 — request the worksheet

**Continue in that same conversation. Use the shorter, natural prompt exactly as shown:**

```text
That looks good. Please prepare a Conference Travel Approval Worksheet for the trip.
```

**Why this prompt is shorter:** The agent instructions already call for retrieving relevant knowledge, and the skill specifies how to gather facts and use the trip details in the current conversation. You do not need to repeat the retrieval instruction or the hotel and dates when requesting the worksheet. The skill still needs to retrieve the relevant knowledge sources.

**Expected:** If the skill is successfully selected and executed, the agent should generate a **CONTOSO — CONFERENCE TRAVEL APPROVAL WORKSHEET** directly in chat, followed by the subtitle **“Advisory assessment only — not an approved travel request or authorization to book.”** Use the trip details established in that conversation.

The expected five assessments are:

| Criterion | Expected status | Why |
| --- | --- | --- |
| Lodging compliance | **PASS** | $225/night is $50 below the $275/night Chicago base-rate limit |
| Budget completeness | **INCOMPLETE** | Taxes, registration, airfare, transport, meals and other costs are unknown |
| Approval status | **PENDING** | No evidence of manager approval |
| Booking information | **INCOMPLETE** | No verified availability, full price, confirmation or cancellation terms |
| Travel preparation | **INCOMPLETE** | Business purpose, full expenses, travel request and remaining checklist steps unresolved |
| **Overall** | **INCOMPLETE** | All readiness criteria have not been satisfied |

This result is **advisory**, not an approval. Producing a worksheet does **not** call a corporate travel system, reserve a room, or charge a card.

### Step 6: Confirm what actually ran

Inspect any skill-use indication or diagnostic details available in your tenant. **Seeing a worksheet in the chat alone doesn't prove that the skill executed**; an agent could imitate the format without calling the packaged skill. If no indicator appears, inspect the skill's configuration and test again. Don't claim confirmed invocation without evidence.

---

## 6. Troubleshooting

| Demo / Section | Symptom | What to check |
| --- | --- | --- |
| All | Can't find **New agent** | Work/school sign-in, administrator policy, eligible license, supported web/desktop UI. |
| Demo 2–3 — Knowledge | Can't access SharePoint knowledge | Site/file permissions, eligible Copilot license or approved PAYG access, admin policies, and whether your files are selected. |
| Demo 2–3 — Knowledge | Newly added SharePoint files do not appear in Cloud files / Work content | Verify SharePoint file access, tenant, licensing and permissions. Allow for indexing/discovery delay. Temporarily use **Attachments** to continue the knowledge exercise; later recheck Work content, remove attachments, connect SharePoint files, and retest in a fresh chat. |
| Demo 2–3 — Knowledge | Attached file shows Preparing, or SharePoint response uses old content | **Preparing** refers to an attachment's processing status where shown; wait for completion. For stale SharePoint results, inspect the actual document, citations and versions, then retry in a fresh conversation. Re-retrieval does not force indexing. |
| Demo 2–3 — Knowledge | It gives an incorrect hotel rate | Check the Word source content, confirm which file is selected, inspect citations, ask the agent to retrieve the relevant source again, and start a fresh conversation if needed. |
| Demo 3 — Skill | Skill **Add** option missing | Verify Skills rollout/eligibility, tenant settings, and any Frontier/preview requirements in current Microsoft docs. |
| Demo 3 — Skill | The worksheet appears in Prompt 1 or 2 | Narrow the skill description: trigger on **explicit worksheet requests only**; make sure you didn't put the worksheet instructions into general agent instructions. |
| Demo 3 — Skill | Prompt 3 doesn't trigger the skill | Check the skill was added and saved, its name/description includes “Conference Travel Approval Worksheet,” and that the same conversation contains prompts 1 and 2. |
| Demo 3 — Skill | First worksheet takes several minutes | Execution time may vary. First runs have sometimes been slower than later ones in the presenter's testing; this is **not proof** of a cold-start mechanism. Retry after testing and allow extra time. |
| Demo 3 — Skill | Want diagnostic details | In Copilot Chat, `-developer on` may enable Developer Mode. A browser **refresh** was needed in the presenter's rehearsal before debug cards appeared. Microsoft does not necessarily expose full internal prompts or skill traces. `-developer off` disables it. |

### Suggested checks for successful reproduction

- [ ] Demo 1 changes the response *format* and handling of unknown company policy without adding knowledge.
- [ ] Demo 2 identifies **three hotels** and compares them against **$275/night**.
- [ ] Demo 2 uses **West Loop Hotel**, October 12–16, **four nights**, **$900 USD**.
- [ ] Demo 3 answers its first two prompts without generating a worksheet.
- [ ] Demo 3's explicit third prompt produces the advisory worksheet with the five assessment categories.
- [ ] The final status is **INCOMPLETE**, not an approval.
- [ ] Citations, permissions, source facts and actual skill invocation are checked, not assumed.

---

## 7. What you should take away

**Instructions** establish role, response style and guardrails; they are not corporate policy data. **Knowledge sources** let the agent retrieve relevant facts from documents the user can access. **Conversation context** keeps details such as a selected hotel available within the ongoing chat, but it is not the same as cross-conversation memory. **A skill** packages the specialized procedure for preparing the worksheet. **Tools** allow agents to interact with external systems and perform actions. In the companion Copilot Studio exercise, an **agent flow is exposed as a tool** to save the worksheet to OneDrive. The Agent Builder worksheet example itself does not save a file or submit an approval.

The example is intentionally modest: three source documents, one agent, three demos, no real-world external actions, and a clear distinction between **helping someone prepare** and **actually approving or booking travel**.

For the current product instructions and prerequisites, check the linked Microsoft Learn articles at the top of this README; Microsoft 365 agent and skill features continue to evolve.
