# Job Fair Aplication API Documentation
API Documentation: Job Fair Application
POST /auth/login
Description: Authenticates an existing user and logs them into the system.
Request Body:

{
  "username": "string",
  "password": "string"
}

Response:
{
  "status": "success"
}


POST /auth/signup
Description: Registers a new user (Employer or Job Seeker) on the platform.
Request Body:
{
  "username": "string",
  "password": "string"
}

Response:
{
  "status": "success"
}



2. Job Listings (for Job Seekers and Employers)
GET /jobs
Description: Displays all available job posts for job seekers to view.
Response:

[
  {
    "title": "string",
    "description": "string",
    "company_name": "string"
  }
]

GET /employer/jobs
Description: Displays job posts specific to the logged-in employer.
Response:

[
  {
    "title": "string",
    "description": "string"
  }
]


3. Employer Features
POST /employer/job
Description: Allows employers to create a new job post.
Request Body:

{
  "title": "string",
  "description": "string",
  "required_skills": "string",
  "salary_range": "string",
  "status": "enabled/disabled"
}

Response:

{
  "status": "success",
  "job_post_id": "integer"
}


GET /employer/job/{job_id}
Description: Retrieves details of a specific job post created by the employer.
Response:

{
  "title": "string",
  "description": "string",
  "required_skills": "string",
  "salary_range": "string",
  "status": "enabled/disabled",
  "applicants": [
    {
      "name": "string",
      "contact_info": "string",
      "cv": "string",
      "status": "approved/rejected/hired"
    }
  ]
}

POST /employer/job/{job_id}/approve_application
Description: Allows the employer to approve a job seeker’s application.
Request Body:

{
  "job_seeker_id": "integer"
}

Response:

{
  "status": "approved"
}


POST /employer/job/{job_id}/reject_application
Description: Allows the employer to reject a job seeker’s application.
Request Body:

{
  "job_seeker_id": "integer"
}

Response:

{
  "status": "rejected"
}


POST /employer/job/{job_id}/hire_application
Description: Marks a job seeker as hired for a specific job post.
Request Body:

{
  "job_seeker_id": "integer"
}

Response:

{
  "status": "hired"
}



4. Job Seeker Features
POST /job_seeker/job/{job_id}/apply
Description: Allows job seekers to apply for a job post.
Request Body:

{
  "cv": "string"  // Job seeker’s CV (optional, can be a link to a file)
}

Response:

{
  "status": "applied"
}

GET /job_seeker/applications
Description: Retrieves all job applications made by the logged-in job seeker, including application status.
Response:

[
  {
    "job_title": "string",
    "company_name": "string",
    "status": "applied/approved/rejected/hired"
  }
]

