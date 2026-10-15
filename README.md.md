# AI Recruitment Screening and Interview Scheduling Automation

Oct 15, 2026 · @mary ramos

## Problem

Hiring teams lose hours to repetitive early-stage work, which slows hiring and makes screening inconsistent. Good candidates are lost to delays.

- Reading every resume against the job requirements
- Sending rejection or follow-up emails by hand
- Writing screening questions for each role
- Going back and forth over interview times
- Keeping candidate status updated in a tracker

## Goal

Automate the path from application to scheduled interview, so recruiters spend time only on pre-qualified candidates.

- Screen every applicant consistently against the job posting
- Respond to every candidate quickly
- Collect screening answers and score them automatically
- Book interviews without manual coordination
- Keep one up-to-date record of every candidate

## Solution

An n8n workflow with five stages, built from the workflow screenshot. Some node labels were small, so confirm the details against the live workflow.

1. **Application intake.** A candidate submits the application form with their resume. The resume is saved to Google Drive and a candidate record is created in Airtable.
2. **Resume screening.** The resume is downloaded and its PDF text extracted. An AI agent (OpenAI) compares it with the matching job posting in Airtable and returns a structured decision. The record is marked Rejected or Potential Hire.
3. **Screening questionnaire.** For potential hires, a second AI agent (Gemini) writes role-specific questions. The candidate gets a follow-up form, and their answers are saved to Airtable.
4. **Personalized outreach.** An AI agent drafts a tailored email using the candidate's record and the job posting, and it is sent through Gmail.
5. **Scoring and interview booking.** Another AI agent evaluates the questionnaire answers. A booking agent then creates a Google Calendar event, and the interview schedule and final status are written back to Airtable.

Structured Output Parsers on each AI step keep results in a predictable format, so later nodes can use them reliably.

## Non-Technical Documentation

### How it works

1. A candidate fills out a job application and uploads their resume.
2. The system reads the resume and checks how well it fits the job.
3. If the fit is poor, the candidate is marked as not moving forward.
4. If the fit is good, the candidate gets a short set of questions tailored to the role.
5. Their answers are reviewed automatically.
6. Qualified candidates receive a personalized email and a calendar invite for an interview.
7. Everything is logged in the hiring tracker, so the team sees each candidate's status at a glance.

### What the recruiter does

- Posts job details in the tracker (Airtable)
- Reviews the candidates who reach the interview stage
- Conducts the interviews

### What the recruiter no longer does

- Reading every resume
- Writing screening questions
- Drafting emails
- Coordinating interview times
- Updating the tracker manually

### Expected benefits

- Faster response times for candidates
- Consistent screening criteria across all applicants
- Far less admin time per hire
- A complete, searchable record of every candidate

### Points to confirm before going live

- Rejections and AI-based decisions should follow your hiring policies and local rules. Many teams add a human review step before final rejections.
- Candidate data (resumes, answers) should be stored and handled according to privacy requirements.

## Tools Used

| Category | Tool |
| --- | --- |
| Automation platform | n8n |
| Application and questionnaire forms | n8n Form Trigger / Form pages |
| File storage | Google Drive |
| Database / candidate tracker | Airtable |
| Resume text extraction | n8n Extract From File (PDF) |
| AI resume screening | OpenAI Chat Model (AI Agent) |
| AI questionnaire, email, scoring and booking | Google Gemini Chat Models (AI Agents) |
| Output formatting | Structured Output Parsers |
| Email | Gmail |
| Scheduling | Google Calendar |
