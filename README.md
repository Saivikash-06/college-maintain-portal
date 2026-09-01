# College Portal — Hackathon Edition

College Portal is a full-stack Smart Academic Management Platform powered by **EduInsight AI**. It includes Student, Teacher, and Admin workspaces with simulated academic intelligence.

## Stack

- Frontend: HTML5, CSS3, Vanilla JavaScript
- Backend: Node.js + Express REST API
- Persistence: `data.json`, generated automatically on first run

## Run locally

1. Install [Node.js LTS](https://nodejs.org/) if it is not already installed.
2. Open a terminal in this folder.
3. Run `npm install`.
4. Run `npm start`.
5. Open `http://localhost:3000`.

Demo credentials:

| Role | ID | Password |
| --- | --- | --- |
| Student | `STU001` | `1234` |
| Teacher | `FAC001` | `1234` |
| Admin | `ADM001` | `1234` |

## Backend modules and API routes

| Project topic | Backend implementation |
| --- | --- |
| Authentication and role access | `POST /api/auth/login`; role middleware protects all dashboards and actions. |
| Student dashboard and AI health | `GET /api/dashboard/student`; server calculates grades, attendance, assignment score, internal marks and trend weights. |
| Teacher dashboard | `GET /api/dashboard/teacher`; returns only students/classes assigned to the logged-in teacher. |
| Admin dashboard | `GET /api/dashboard/admin`; returns institution-level demo data. |
| Student ID search | `GET /api/students/:id`; teacher class authorization is enforced. |
| Assignment creation/edit/delete | `POST`, `PUT`, `DELETE /api/assignments`; new assignments appear automatically for eligible students. |
| Student submission | `POST /api/assignments/:id/submit`; stores comment, simulated filename and submission status. |
| Teacher evaluation and score validation | `POST /api/assignments/:id/evaluate/:studentId`; rejects scores outside `0..maxScore`, updates subject performance and creates a notification. |
| Attendance | `POST /api/attendance`; updates each student’s selected subject attendance. |
| Risk center | Server computes `HIGH RISK`, `NEEDS ATTENTION`, or `STABLE` from score and attendance. |
| AI chat | `POST /api/ai/chat`; returns data-backed academic answers for student/teacher questions. |
| Notifications | `GET /api/notifications`; submission and evaluation events generate role-relevant messages. |

## Data flow

Teacher creates assignment → eligible student sees and submits it → teacher evaluates it → backend validates and saves the score → student’s subject score/trend, AI health and notification update automatically.

## Important hackathon note

This is a demo implementation. Its authentication token and `data.json` storage are intentionally simple, and the EduInsight scoring model is illustrative only. For production, use password hashing, a real database, proper signed sessions/JWTs, validation, audit logging and a reviewed academic-decision policy.
