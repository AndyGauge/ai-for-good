# Cue

A district manager walks into Monday morning with four hundred people on her roster.

Eighty of them missed a shift last week. Twelve are in onboarding and halfway through their paperwork. Six properties are behind on interview scheduling. Two locations are flagged red in a dashboard she does not have time to open.

What she has time to do is text.

## The dashboard trap

A dashboard shows you the business. It does not run the business.

You stare at the red tile. You screenshot it into Slack. You tab into the HR system to pull a list of names. You tab into the scheduling tool to reassign shifts. You tab into the hiring system to open new job reqs. You tab into the onboarding tracker to send reminders. Five tools, four tabs, one text to the regional VP.

Then you do it again tomorrow.

Dashboards were supposed to make this faster. They made it smarter. They did not make it fewer steps. The manager who has four hundred reports is still the one opening five tools to fix one problem.

## The shift

The chat presents the findings. It recommends the actions. You click the button.

Not a dashboard. Not a chart. Not a link to another tool. A plain-language summary and a set of buttons written in the manager's own words.

> Dallas is short on Saturday.

Cue reads the current staffing numbers. It checks the hot-lead pool. It looks at tomorrow's calendar. Then it replies in the manager's own language:

*Saturday at Dallas is short by four. Twenty-seven candidates in the hot-lead pool match the role. Interviews can run tonight and tomorrow morning.*

Below the reply, three buttons.

**[Post 5 Jobs at Dallas]**

**[Invite 27 Candidates]**

**[Schedule Tonight's Interviews]**

The buttons are written the way the manager speaks. Not *POST_REQ_BATCH(5)*. Not *ATS.invite_candidates(27)*. Not *submit form 5b*. Post five jobs at Dallas. Invite twenty-seven candidates. The label for a PTO approval is **Approve Time Off**. The label for a calendar hold is **Make New Event**. Whatever the action is, described the way the person actually talks about it.

The manager taps. Cue does the work. It reports back in the thread.

The agent proposes. The human signs.

This is what Fountain launched in April 2026. They call it [Cue](https://www.fountain.com/). The phrase inside the company, roughly: *run your business with the intelligence, not just see it.*

That one phrase is the whole distinction this chapter is about.

## Zoomed in: Hire Go

Cue is the district manager's tool. [Hire Go](https://www.fountain.com/hire-go) is the same pattern at the property.

A hotel general manager at an Aimbridge property is not a recruiter. She runs the front desk, the housekeeping team, the night shift, the banquet crew. When she loses a housekeeper on Friday, she needs a new one on Monday. The old way says *file a req with corporate recruiting, wait, and hope*. The new way is conversation.

The GM opens the app on her phone. She says *I need a housekeeper for a Monday start.* Hire Go reads the last batch of leads she reviewed, checks her Tuesday calendar, and replies with a draft posting, three candidates, and two interview slots that clear her all-hands. Three buttons, in her words: **Post the housekeeper role. Invite these three. Schedule interviews at 2 and 4.** She taps. The job is posted. The interviews are on her calendar. She never opens a separate hiring tool. She never talks to a recruiter.

Aimbridge runs hiring through this interface at every one of its fifteen hundred properties.

[Anthropic's 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report) profiles the implementation on page eight. Fifty percent faster screening. Forty percent faster onboarding. Candidate conversion doubled. The architecture underneath is Claude-driven multi-agent orchestration — several specialized agents, each with one job, coordinated by an orchestrator that reads the manager's text.

## Why this is not BI

BI shows you the number. BI does not change the number.

Every text-to-SQL product, every conversational dashboard, every *just ask your data* tool built on top of Snowflake or Looker or Power BI — they all stop at the same place. They show you the answer. Then you go do something with it.

Cue does not stop there. Hire Go does not stop there.

The manager tells it what she needs. The system drafts the actions, labels them in her own words, and waits for the tap. She taps. The work is done. The distinction matters because a frontline manager does not have bandwidth for an extra step that says *now open these five tools*. The bandwidth tax is where the operational leverage evaporates.

You do not solve the frontline manager's problem by giving her a better window. You solve it by giving her a pair of hands that wait for her signal.

## The honest part

A pair of hands is a dangerous thing to hand to an LLM.

So you gate. Actions that write to the system are logged. Actions that cost money require a budget envelope the manager has already set. Actions that affect a person — firing, discipline, reducing hours — require human approval at every step, every time, with no default-yes. The model drafts. The human signs.

You publish the list of actions the agent can take without approval, the list it requires approval for, and the list it is flat out not allowed to touch. The manager knows. The compliance officer knows. The employee knows.

You audit. You log the prompt, the actions taken, the outcome, the approvals given. When HR asks *why was this shift reassigned*, you show them the prompt and the approval chain. In English.

Agentic tooling that bypasses these gates is the failure mode that gives all of this a bad name. Do not build that. Do not ship that. If you work at a company that is shipping that, leave.

## The pattern

Writing the rules is infinite. Writing the intent is a paragraph. The paragraph is maintained by the person who already knew what it should say.

At this scale, the person who knows is the manager. The district manager has been running a region for eleven years. The hotel GM has been running that property for three. They know what the data means. They do not need a better dashboard. They need a system that executes their judgment when they tell it to.

That is what Cue is. That is what Hire Go is.

Same pattern as the address field. Same pattern as the interview. The intent is in English. The execution is in software. The domain owner owns the fix.

This time, the domain owner is running a region. Or a hotel. Or fifteen hundred hotels from a phone on a Friday afternoon.
